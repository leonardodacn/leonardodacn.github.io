# mybatis 增加自定义拦截器


MyBatis 提供的强大机制，使用插件是非常简单的，只需实现 Interceptor 接口，并指定想要拦截的方法签名即可。

## 拦截器

```java
import java.text.DateFormat;
import java.util.Date;
import java.util.List;
import java.util.Locale;
import java.util.Properties;

import org.apache.ibatis.executor.Executor;
import org.apache.ibatis.mapping.BoundSql;
import org.apache.ibatis.mapping.MappedStatement;
import org.apache.ibatis.mapping.ParameterMapping;
import org.apache.ibatis.plugin.Interceptor;
import org.apache.ibatis.plugin.Intercepts;
import org.apache.ibatis.plugin.Invocation;
import org.apache.ibatis.plugin.Plugin;
import org.apache.ibatis.plugin.Signature;
import org.apache.ibatis.reflection.MetaObject;
import org.apache.ibatis.session.Configuration;
import org.apache.ibatis.session.ResultHandler;
import org.apache.ibatis.session.RowBounds;
import org.apache.ibatis.type.TypeHandlerRegistry;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

@Intercepts({  
	@Signature(type = Executor.class, method = "update", args = { MappedStatement.class, Object.class }),  
    @Signature(type = Executor.class, method = "query",  args = { MappedStatement.class, Object.class, RowBounds.class, ResultHandler.class }) 
})  
public class MybatisInterceptor implements Interceptor {
	
	private static final Logger log = LoggerFactory.getLogger(MybatisInterceptor.class);

	@Override
	public Object intercept(Invocation invocation) throws Throwable {
		MappedStatement mappedStatement = (MappedStatement) invocation.getArgs()[0];  
        Object parameter = null;  
        if (invocation.getArgs().length > 1) {  
            parameter = invocation.getArgs()[1];  
        }  

        BoundSql boundSql = mappedStatement.getBoundSql(parameter);  
    	Configuration configuration = mappedStatement.getConfiguration();  
    	Object returnVal = invocation.proceed();
   
    	//获取sql语句
   	 	String sql = getSql(configuration, boundSql);  
    	log.info("Mybatis 拦截器获取SQL:{}",sql);
    	return returnVal;
	}

	@Override
	public Object plugin(Object target) {
		 return Plugin.wrap(target, this);
	}

	@Override
	public void setProperties(Properties arg0) {
	}
	
	/**
	 * 获取SQL
	 */
	private String getSql(Configuration configuration, BoundSql boundSql) {
		Object parameterObject = boundSql.getParameterObject();  
	    List<ParameterMapping> parameterMappings = boundSql.getParameterMappings();  
	    String sql = boundSql.getSql().replaceAll("[\\s]+", " ");  
	    if (parameterObject == null || parameterMappings.size() == 0) {
	    	return sql;
	    }  
        TypeHandlerRegistry typeHandlerRegistry = configuration.getTypeHandlerRegistry();  
        if (typeHandlerRegistry.hasTypeHandler(parameterObject.getClass())) {  
        	sql = sql.replaceFirst("\\?", getParameterValue(parameterObject));  
        } else {  
        	MetaObject metaObject = configuration.newMetaObject(parameterObject);  
            for (ParameterMapping parameterMapping : parameterMappings) {  
            	String propertyName = parameterMapping.getProperty();  
                if (metaObject.hasGetter(propertyName)) {  
                	Object obj = metaObject.getValue(propertyName);  
                    sql = sql.replaceFirst("\\?", getParameterValue(obj));  
                } else if (boundSql.hasAdditionalParameter(propertyName)) {  
                	Object obj = boundSql.getAdditionalParameter(propertyName);  
                	sql = sql.replaceFirst("\\?", getParameterValue(obj));  
                }  
            }  
        }  
	    return sql;
	}

	private String getParameterValue(Object obj) {  
		String value = null;  
		if (obj instanceof String) {  
			value = "'" + obj.toString() + "'";  
	    } else if (obj instanceof Date) {  
	        DateFormat formatter = DateFormat.getDateTimeInstance(DateFormat.DEFAULT, DateFormat.DEFAULT, Locale.CHINA);  
	        value = "'" + formatter.format(obj) + "'";  
	    } else {  
	        if (obj != null) {  
	            value = obj.toString();  
	        } else {  
	            value = "";  
	        }  
	    }  
	    return value;  
	}  
}
```

## 配置

```yml
mybatis:
  type-aliases-package: me.zingon.pagehelper.model
  mapper-locations: classpath:mapper/*.xml
  configuration:
    map-underscore-to-camel-case: true
    default-fetch-size: 100
    default-statement-timeout: 30
```

在springboot中要给mybatis加上这个拦截器，有三种方法，前两种方法在启动项目时不会自动调用自定义拦截器的setProperties方法。

### 第一种

直接给自定义拦截器添加一个 @Component注解，当调用sql时结果如下，可以看到拦截器生效了，但是启动时候并没有自动调用setProperties方法。

### 第二种

在配置类里添加拦截器，这种方法结果同上，也不会自动调用setProperties方法。

```java
@Configuration
public class MybatisConfig {
    @Bean
    ConfigurationCustomizer mybatisConfigurationCustomizer() {
        return new ConfigurationCustomizer() {
            @Override
            public void customize(org.apache.ibatis.session.Configuration configuration) {
                configuration.addInterceptor(new MyPageInterceptor());
            }
        };
    }
}
```

### 第三种

这种方法就是跟以前的配置方法类似，在yml配置文件中指定mybatis的xml配置文件,注意config-location属性和configuration属性不能同时指定

```yml
mybatis:
  config-location: classpath:mybatis.xml
  type-aliases-package: com.haokiu.model
  mapper-locations: classpath:mapper/*.xml
```

mybatis.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <typeAliases>
        <package name="com.haokiu.model"/>
    </typeAliases>
    <plugins>
        <plugin interceptor="com.haokiu.interceptor.MyInterceptor"> 
            <property name="dialect" value="oracle"/>
        </plugin>
    </plugins>
</configuration>
```

可以看到，在启动项目的时候setProperties被自动调用了

## 总结

前两种方法可以在初始化自定义拦截器的时候通过 @Value 注解直接初始化需要的参数。
