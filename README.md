# Vue项目疫情展示

## 知识点
1. Vue基础知识
2. Axios网络请求
3. Echarts可视化
4. Swiper焦点轮播图
5. Vue-Router
6. 封装组件

## 效果参考地址
http://iwenwiki.com/webdoc/17Vue%E6%A8%A1%E5%9D%97/#%E9%A1%B9%E7%9B%AE%E7%9F%A5%E8%AF%86%E7%82%B9

## 可使用地址
用友：https://api.yonyoucloud.com/apilink/#/
天行：https://www.tianapi.com/

## 安装依赖
```js
npm install --save axios
```

## 开发过程中的思维方式
1. 在Vue框架中，是组件式开发，将组件分离的更加细致一点


## 关于组件实例化问题！
1. 拆分中组件之后，组件的多次调用，会每一次实例化一个独立的对象

## 打包
1. 打包命令
```js
npm run build
```
2. 打包之后预览
```js
npm install -g serve
serve -s dist
```
3. 跨域问题
    - 开发环境
        开发环境下的跨域处理，只能在开发环境下运行，打包之后是不能运行的
        proxy都是开发环境跨域
    - 生产环境
        cors(主)
        jsonp
4. 打包路径问题
    publicPath指定具体子路径信息
    ```js
    publicPath: process.env.NODE_ENV === 'production' ? '/covid19' : '/'
    ```