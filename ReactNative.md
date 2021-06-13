> ```js
>  react-native bundle --entry-file index.js --bundle-output `pwd`/out/ios/main.jsbundle --platform ios --assets-dest `pwd`/out/ios --dev false
> 
> --dev 如果为false，那么会压缩
> ```

Button的onpress事件内的方法可以写两种：第一种onpress={()=>this.abc()} 第二种 onpress={this.abc.bind(this)}