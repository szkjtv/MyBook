## GoWebCRUD

导入必须要导入的包

```go
import (
	"database/sql"
	"html/template"
	"log"
	"net/http"

	_ "github.com/go-sql-driver/mysql"
)
```

数据库初始化依依对应相对应的表

```go
type Employee struct {
	Id    int
	Name  string
	City  string
	Age   int
	Sex   string
	Email string
}

//连接数据库
func dbConn() (db *sql.DB) {
	dbDriver := "mysql"   //数据库mysq类型
	dbUser := "root"  	//数据库连接名称
	dbPass := "aa1451418"	//数据库登录密码
	dbName := "class_test"	//数据库（表）名
	db, err := sql.Open(dbDriver, dbUser+":"+dbPass+"@/"+dbName)
	if err != nil {
		panic(err.Error())
	}
	return db
}


//用tmpl初始化模板文件
var tmpl = template.Must(template.ParseGlob("tmpl/*"))

//起动默认文件首页文件
func New(w http.ResponseWriter, r *http.Request) {
	tmpl.ExecuteTemplate(w, "New", nil)
}

//接入数据到数据库中去
func Insert(w http.ResponseWriter, r *http.Request) {
	db := dbConn()
	if r.Method == "POST" {
		name := r.FormValue("name")  //对应数据库（名字）
		city := r.FormValue("city")//对应数据库（城市）
		age := r.FormValue("age")//对应数据库（年龄）
		sex := r.FormValue("sex")//对应数据库（性别）
		email := r.FormValue("email")//对应数据库（邮箱）
		insForm, err := db.Prepare("INSERT INTO Employee(name, city, age,sex,email) VALUES(?,?,?,?,?)")  //这个也要加上数据库相对应的字段
		if err != nil {
			panic(err.Error())
		}
		insForm.Exec(name, city, age, sex, email)
		log.Println("INSERT: Name: " + name + " | City: " + city)
	}
	defer db.Close()
	http.Redirect(w, r, "/", 301) //重定向到默认的（/）首页
}

//main入口包
func main() {
    http.Handle("/static/", http.StripPrefix("/static/", http.FileServer(http.Dir("static")))) //启动静态服务
	log.Println("Server started on: http://localhost:8080")
	http.HandleFunc("/new", New)
	http.HandleFunc("/insert", Insert)  //action="insert"这里是前端form表单上对应的
	http.ListenAndServe(":8080", nil)
}


```

这是New.thml文件

```html
{{ define "New" }} //这里必须加入才能成功显示前端页面
   <h2>New Name and City</h2>  
    <form method="POST" action="insert">  //action需要对应路由的信息
      <label> Name </label><input type="text" name="name" /><br /> //这是数据库（名称）
      <label> City </label><input type="text" name="city" /><br />//这是数据库（城市）
      <label> Sex </label><input type="text" name="sex" /><br />//这是数据库（性别）
      <label> Age </label><input type="text" name="age" /><br />//这是数据库（年龄）
      <label> Email </label><input type="text" name="email" /><br />//这是数据库（邮箱）
      <input type="submit" value="Save user" />
    </form>
{{ end }} //这里也是必须的
```

