### webpack
核心就是一个打包器,它能够识别文件中的require export imprort等语句(amd/cmd/es6 module),从而能够识别文件的依赖关系,然后通过注入代码的方式,生成浏览器能够识别的依赖关系代码。
在分析依赖文件的时候,通过配置文件中配置的一些laoder(babel、minify等),对文件内容进行预处理。  

### babel
就是一个转译器平台,自身不提供转译功能,需要转译插件配合。将源语法转移成目标语法。  


### gulp + webpack 
就是使用通过gulp插件gulp-webpack来实现,该插件使用gulp实现方式对webpack进行封装。使其可以在gulp的管道流中被使用。  
```
//处理js文件
gulp.task("js", function () {
    var glob = bPath.jsGlobPath;
    return gulp.src(glob, {base : bPath.jsSrcRootPath})
        .pipe(webpack({   //此webpack实例是gulp的一个插件gulp-webpack
            output: {
                path : bPath.jsSrcRootPath, //必须配置，否则js文件的根路径为当前构建器所在的根路径
                filename: '[name]',
                chunkFilename : '[name]?v=[hash]'
            },
            resolve : {
                root : bPath.jsSrcRootPath
            },
            resolveLoader: { root: [path.join(__dirname, "node_modules"), __dirname] }, //指定loader路径
            module: {
                loaders: [
                    {test: /\.html$/, loader: 'raw-loader!html-minify'},
                    { test: /\.js$/, loader: 'module-path!babel?plugins[]=babel-plugin-transform-es2015-arrow-functions'}
                ]
            },
            //keep comments for avalon ms-for
            'html-minify-loader': {
                comments: true
            }
        }))
        .pipe(uglify()) //混淆
        .pipe(gulp.dest(bPath.jsDistRootPath)); //打包
});
```

### 遇到的坑:  
- webpack必须是gulp任务的第一个处理pipe,因为webpack入口不是以内容流的方式输入的,而是以文件名,所以会忽略前面pipe的处理
- webpack中,如果一个test使用了多个loader,则不能使用query属性,loader的参数需要通过querystring的方式配置