# go 匿名结构体 数组 示例


在用 vscode 生成测试用例的时候，生成了测试的匿名数组，没怎么用过，这里展示了 go 匿名结构体数组示例
```
import "testing"

func TestGetRandomString(t *testing.T) {
	type args struct {
		lens int
	}
	tests := []struct {
		name string
		args args
		want string
	}{
		{
			name: "test",
			args: args{
				lens: 6,
			},
			want: "hi",
		},
		{
			name: "test",
			args: args{
				lens: 6,
			},
			want: "hi",
		},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := GetRandomString(tt.args.lens); got != tt.want {
				t.Logf("GetRandomString() = %v, want %v", got, tt.want)
			}
		})
	}
}

```

需要注意的是各个结构体后面有个逗号。
