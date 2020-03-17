1、创建项目文件夹demo，进入文件夹下运行： 
`go mod init demo` 
会在demo文件夹下新增一个go.mod的文件，不要手动修改

2、在main.go或其他项目文件中，正常引用第三方的包，然后在demo目录下执行:
`go run main.go`
会自动将依赖的第三方包下载下来，并且把依赖加到go.mod文件中