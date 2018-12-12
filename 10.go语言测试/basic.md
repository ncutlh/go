# 10.go语言测试

## 表格驱动测试
    import "testing"
    
    func TestTriangle(t *testing.T) {
    	tests := []struct{ a, b, c int }{
    		{3, 4, 5},
    		{5, 12, 13},
    		{8, 15, 17},
    		{12, 35, 37},
    		{30000, 40000, 50000},
    	}
    
    	for _, tt := range tests {
    		if actual := calcTriangle(tt.a, tt.b); actual != tt.c {
    			t.Errorf("calcTriangle(%d, %d); "+
    				"got %d; expected %d",
    				tt.a, tt.b, actual, tt.c)
    		}
    	}
    }
    
## 工具 
### 覆盖测试 go tool cover -html=c.out
### 性能测试 go test -bench .
### 性能优化 go test -bench . -cpuprofilecpu.out
      go tool pprof cpu.out 
      输入： 
         web
     需要安装工具