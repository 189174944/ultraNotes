```
import "github.com/gin-gonic/gin"

func main() {
	r := gin.Default()
	r.GET("/ping", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "pong",
		})
	})
	r.Run("127.0.0.1:8081") // listen and serve on 0.0.0.0:8080
}
```



GO语言ORM框架的使用

```
go get github.com/jinzhu/gorm
go get github.com/go-sql-driver/mysql
```

