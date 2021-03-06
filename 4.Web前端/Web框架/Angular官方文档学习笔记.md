# Angular

**Angular 是什么**：

[Angular](https://www.angular.cn/) 是由谷歌开发与维护一个开发跨平台应用程序的框架，同时适用于手机与桌面。

**Angular 有什么特点**：

- 基于 Angular 我们可以构建适用于所有平台的应用。比如：Web 应用、移动 Web 应用、移动应用和桌面应用等。
- 通过 Web Worker和服务端渲染 (SSR)，达到在如今Web平台上所能达到的最高渲染速度。
- Angular 让你能够有效掌控可伸缩性。基于 RxJS、Immutable.js 和其它推送模型，能适应海量数据需求。

**Angular 提供了哪些功能**：

- 动态HTML
- 强大的表单系统 (模板驱动和模型驱动)
- 强大的视图引擎
- 事件处理
- 快速的页面渲染
- 灵活的路由
- HTTP 服务
- 视图封装
- AOT、Tree Shaking

**Angular 与 AngularJS 有什么区别**：

- 不再有`Controller`和 `Scope`。
- 更好的组件化及代码复用。
- 更好的移动端支持。
- 引入了 `RxJS` 与 `Observable`。
- 引入了 `Zone.js`，提供更加智能的变化检测。

### Angular 配置环境

**基于 Angular Quickstart**：

使用 Git 克隆：

```
git clone https://github.com/angular/quickstart ng4-quickstart
```

安装依赖：

```
npm install
```

**基于 Angular CLI**：

安装 Angular CLI：

```
npm install -g @angular/cli
```

检测是否安装成功：

```
ng --version
```

创建新项目：

```
ng new PROJECT-NAME
```

启动本地服务器：

```
cd PROJECT-NAME
ng serve
```

### 自定义组件

创建新组件：

```
ng generate component COMPONENT-NAME
```

定义组件元信息：

```
@Component({
   selector: 'app-component-name',  // 用于定义组件在HTML代码中匹配的标签
   templateUrl: './component-name.component.html', // 定义组件的模板视图文件路径
   styleUrls: ['./component-name.component.css']  // 定义组件的样式文件路径
})
```

定义组件类：

```
export class Student  {
  name = 'zhangsan'; 
}
```

### 路由

导入路由模块：

```typescript
import { RouterModule } from '@angular/router';

@NgModule({
  imports: [RouterModule,...],
  ...
})
export class AppModule { }
```

配置路由信息：

```typescript
import { Routes, RouterModule } from '@angular/router';
import { UserComponent } from './user.component';

export const ROUTES: Routes = [
  { path: 'user', component: UserComponent }
];

@NgModule({
  imports: [
    BrowserModule,
    RouterModule.forRoot(ROUTES)
  ],
  // ...
})
export class AppModule {}
```

routerLink 指令：链接到相应组件。

```html
<a routerLink="/">首页</a>
<a routerLink="/user">我的</a>
```

router-outlet 指令：此处加载组件

```
<router-outlet></router-outlet>
```

## 架构

一个 Angualr 应用的基本构造块是 `NgModule` ，它为组件提供了编译的上下文。一个 Angular 应用是由一组 `NgModule` 定义出来的。

- 组件定义**视图**。
- 组件使用**服务**（服务作为**依赖**被**注入**到组件中）。

组件与服务都是简单类，使用装饰器标注它们的类型，并提供元数据告知 Angular 如何使用它们。

- 组件类(@Component)元数据：关联组件类与视图模板 (template) 。

- 服务类(@Injectable)元数据：提供了一些信息，Angular 要用这些信息来让组件可以通过*依赖注入（DI）*使用该服务。
- 路由服务：定义视图间的导航路径。

**模块**：

NgModule 可以将其组件和一组相关代码（如服务）关联起来，形成功能单元。

每个应用都有一个根模块 (AppModule) 。根模块提供了用来启动应用的引导机制。 一个应用通常会包含很多功能模块。

NgModule 也可以从其它 NgModule 中导入功能，并允许导出它们自己的功能供其它 NgModule 使用。

**组件**：模板、指令和数据绑定。

使用 `@Component()` 装饰器标注组件，每个应有至少有一个根组件。

**模板、指令和数据绑定**：

- 属性绑定：组件输入数据，将应用数据中的值插入视图。
- 事件绑定：组件输出数据，应用接受模板中的数据。

**服务与依赖注入**：

服务：与视图无关，跨组件共享数据与逻辑。

依赖注入：服务作为依赖被注入到组件中。

**路由**：路由器会将URL路径映射到视图。

### 模块简介（NgModule）

Angular 应用是模块化的。

一个 NgModule 就是一个容器，用于存放一些内聚的代码块，这些代码块专注于某个应用领域、某个工作流或一组紧密相关的功能。 它可以包含一些组件、服务提供商或其它代码文件，其作用域由包含它们的 NgModule 定义。 它还可以**导入**一些由其它模块中导出的功能，并**导出**一些指定的功能供其它 NgModule 使用。

每个Angular应用至少包含一个根模块 (AppModule) ，位于 `app.module.ts` 文件中，引导根模块即可启动应用。

**@NgModule 元数据**：

`@NgModule()`：NgModule 装饰器；

- declaration (可声明对象) - 声明属于本 NgModule 的组件、指令、管道。
- import (导入模块) - 本 NgModule 导入的其他模块。
- export (导出模块) - 本 NgModule 导出的可在其他模块的组件模板中使用的可声明对象的子集。
- providers (服务提供商) - 模块级别的服务提供商，全局服务提供商。
- bootstrap (根组件) - 只有根模块设置 bootstrap 属性。

**NgModule 与组件**：

NgModule 为其中的组件提供了一个*编译上下文环境*。

组件与模板共同定义了视图，组件还可以包含视图层次结构。

**NgModule 与 JavaScript**：

NgModule 系统与 JavaScript（ES2015）用来管理 JavaScript 对象的模块系统无关。

### 组件简介（Component）

组件控制屏幕上称为视图的一小片区域。

组件通过一些由属性和方法组成的 API 与视图交互。

**@Component 元数据**：

`@Component()`：组件装饰器；

- selector - 一个 CSS 选择器，在HTML中选择器对应的标签中插入该组件。
- templateUrl - 组件 HTML 模板文件的相对路径。
- providers：当前组件的服务提供商。

**模板语法**：

- 数据绑定 - 协调应用与 DOM 中的数据，（`{{hero.name}}`，`(click)`，`[hero]`）。

- 管道：数据转换。

- 指令：程序逻辑应用到视图上，（`*ngIf`，`*ngFor`，`NgModel`）。

**数据绑定**：

- 插值表达式：`{{value}}`；（组件 --> DOM）
- 属性绑定：`[prop] = "value"`；（组件 --> DOM）
- 事件绑定：`(event) = "handler"`；（组件 <-- DOM）
- 双向绑定：`[(ngModel)] = "property"`；（组件 <--> DOM）

> - 父组件 --> 子组件：属性绑定。
> - 子组件 --> 父组件：事件绑定。

**管道**：

管道 (Pipe) ：值的转换逻辑。

管道使用：`{{ value | pipe }}`；

管道声明：`@Pipe()` 管道装饰器；

**指令**：

Angular 模板是动态的，Angular 渲染时，根据指令对 DOM 进行转换。

指令分为结构型指令和属性型指令。

- 结构型指令：`*ngIf`，`*ngFor`，`*ngSwitch`。
- 属性型指令：`ngModel`，`NgClass`，`NgStyle`。

### 服务（Service）

理想情况下，组件的工作只管用户体验，把诸如从服务器获取数据、验证用户输入或直接往控制台中写日志等工作委托给各种服务。

Angular 通过依赖注入将服务注入到组件中。

`@Injectable()` ：服务装饰器。

### 后续

响应式编程：

- 生命周期钩子：通过实现生命周期钩子接口，可以监听组件生命周期中的一些关键时刻，从创建到销毁。
- 可观察对象：在组件和服务中使用可观察对象来发布和订阅任意类型的消息。

客户端与服务器交互：

- HTTP：用 HTTP 客户端与服务器通讯，以获取数据、保存数据或执行服务端动作。
- 服务端渲染：Angular Universal 会通过服务端渲染（SSR）技术在服务器上生成静态的应用页面。
- Service Worker：借助 Service Worker 来减轻对网络的依赖，你可以显著提升用户体验。

特定库：

- 动画：Angular 动画库
- Forms：基于 HTML 的验证和脏数据检查。

开发：

- 编译：Angular 为开发环境提供了 JIT（即时）编译方式，为生产环境提供了 AOT（预先）编译方式。
- 测试：对应用的各个部件运行单元测试。

环境搭建：

- CLI命令参考手册：
- 工作空间与文件结构：
- npm包：

## 组件与模板

创建新组件：

```shell
ng generate component COMPONENT-NAME
```

定义组件元信息：

```ts
@Component({
   selector: 'app-component-name',  // 用于定义组件在HTML代码中匹配的标签
   templateUrl: './component-name.component.html', // 定义组件的模板视图文件路径
   styleUrls: ['./component-name.component.css']  // 定义组件的样式文件路径
})
```

定义组件类：

```ts
export class Student  {
  name = 'zhangsan'; 
}
```

### 显示数据

1.使用插值表达式：`{{ value }}`。

2.使用内联模板（`template`）或模板文件（`templateUrl`）。

3.使用 `*ngIf` 条件显示：

```html
<p *ngIf="heroes.length > 3">There are many heroes!</p>
```

4.使用 `*ngFor` 循环显示：

```html
<ul>
  <li *ngFor="let hero of heroes">
    {{ hero.name }}
  </li>
</ul>
```

### 模板语法

`<script>` 是无效的，它被忽略了。

`<html>`、`<body>` 和 `<base>` 是无意义的。

**插值表达式**：`{{ value }}` 

- 可进行求值计算。
- 可调用宿主组件的方法。

> 插值表达式是一种特殊语法，Angular 将其转换为了属性绑定。

**模板表达式**：属性绑定使用

模板**表达式**产生一个值。Angular 执行这个表达式，并把它赋值给绑定目标的属性，这个绑定目标可能是 HTML 元素、组件或指令。在插值表达式/属性绑定中常用到模板表达式。

表达式上下文就是这个组件实例。表达式中的上下文变量是由*模板变量*、*指令的上下文变量*（如果有）和*组件的成员*叠加而成的。（模板变量 > 指令上下文变量 > 组件成员变量）。

> 模板表达式是没有可见的副作用，模板表达式除了目标属性的值以外，不应该改变应用的任何状态。这条规则是 Angular “单向数据流”策略的基础。

JavaScript 中那些具有或可能引发副作用的表达式是被禁止的：

- 赋值 (`=`, `+=`, `-=`, ...)
- `new` 运算符
- 使用 `;` 或 `,` 的链式表达式
- 自增和自减运算符：`++` 和 `--` 
- 不支持位运算 `|` 和 `&` 

**模板语句**：事件绑定使用

模板语句用来响应由绑定目标（如 HTML 元素、组件或指令）触发的事件 `(event)="statement"` 。

模板上下文的变量名 > 组件上下文中的变量名。

> 模板语句是有副作用的。 这是事件处理的关键。因为你要根据用户的输入更新应用状态。响应事件是 Angular 中“单向数据流”的另一面。 在一次事件循环中，可以随意改变任何地方的任何东西。

#### 数据绑定

- 插值表达式：`{{value}}`；（组件 --> DOM）
- 属性绑定：`[prop] = "value"`；（组件 --> DOM）
- 事件绑定：`(event) = "handler"`；（组件 <-- DOM）
- 双向绑定：`[(ngModel)] = "property"`；（组件 <--> DOM）

数据绑定不是设置 HTML attr，而是设置 DOM 元素、组件和指令的 prop。

**HTML attr 与DOM prop **：

- attr 值不可改变，指定初始值；prop 值可以改变，指定当前值。

- 在 Angular 中，attribute 唯一的作用是用来初始化元素和指令的状态。当进行数据绑定时，只是在与元素和指令的 property 和事件打交道。

**attribute、class、style 绑定**：

- attribute 绑定：`[attr.colspan]="value"` 。
- css 绑定：`[class.class-name]="逻辑表达式"` 。（一般用 NgClass）
- style 绑定：`[style.style-prop]="逻辑表达式"` 。（一般用 NgStyle）

> 当元素没有属性可绑的时候，就必须使用 attribute 绑定。

**$event 和事件处理语句**：

$event：事件载荷，由 EventEmitter 实例的 emit() 方法抛出的数据。通过 $event 事件对象传递关于此事件的信息 (数据值) 。

事件属于指令，自定义事件即一个 Angular EventEmitter 实例。指令调用 `EventEmitter.emit(payload)` 来触发事件，可以传入任何东西作为消息载荷。

**双向数据绑定**：

`[(x)]="value"` 本质即 `[x]="value"` 和 `(xChange)="value=$event"` 的结合。

```ts
@Input [x]: any
@Output (xChange)= new EventEmitter<any>()
```

> 原生 HTML 元素不遵循 `x` 值和 `xChange` 事件的模式，但 Angular 以 NgModel 指令为桥梁，允许在表单元素上使用双向数据绑定。

#### 内置指令

**内置属性性指令**：

ngClass：添加或移除一组 CSS 类。

```html
<div [ngClass]="currentClasses"></div
```

```ts
this.currentClasses =  {
  'saveable': this.canSave,
  'modified': !this.isUnchanged,
  'special':  this.isSpecial
};
```

ngStyle：添加或移除一组 CSS 样式。

```html
<div [ngStyle]="currentStyles"></div>
```

```ts
this.currentStyles = {
  'font-style':  this.canSave      ? 'italic' : 'normal',
  'font-weight': !this.isUnchanged ? 'bold'   : 'normal',
  'font-size':   this.isSpecial    ? '24px'   : '12px'
};
```

ngModel： 双向绑定到 HTML 表单元素。

```html
<input [(ngModel)]="currentHero.name">
```

```html
<input [ngModel]="currentHero.name"
  (ngModelChange)="currentHero.name=$event">
```

**内置结构性指令**：

*ngIf：条件展示。

```html
<div *ngIf="currentHero">Hello, {{currentHero.name}}</div>
```

> 防范空指针异常。

*ngFor：循环展示。

```html
<div *ngFor="let hero of heroes">{{hero.name}}</div>
```

> 使用 let 创建了一个名为 hero 的模板输入变量。

```html
<div *ngFor="let hero of heroes; let i=index">{{i + 1}} - {{hero.name}}</div>
```

> 通过模板输入变量捕获索引 `index` 的值。

*ngSwitch：

```html
<div [ngSwitch]="currentHero.emotion">
  <app-happy-hero *ngSwitchCase="'happy'" [hero]="currentHero"></app-happy-hero>
  <app-sad-hero *ngSwitchCase="'sad'" [hero]="currentHero"></app-sad-hero>
  <app-confused-hero *ngSwitchCase="'confused'" [hero]="currentHero"></app-confused-hero>
  <app-unknown-hero *ngSwitchDefault [hero]="currentHero"></app-unknown-hero>
</div>
```

#### 其他语法

**模板引用变量**：

模板引用变量（`#var` / `ref-var`）：通常用来引用模板中的某个 DOM 元素。

示例：

```
<input #box (keyup)="onKey(box.value)">
```

**输入输出属性**：

- 输入属性：带有 `@Input` 装饰器的可设置属性。通过属性绑定的方式使值流入属性。
- 输出属性：带有 `@Output` 装饰器的可设置属性。通过事件绑定的方式使值流出属性。

> 外部组件应该只能绑定到组件的公共（允许绑定） API 上。
>
> TypeScript 的 `public` 是没用的。

1、直接声明输入输出属性：

```ts
@Input('alias')  hero: Hero;
@Output() deleteRequest = new EventEmitter<Hero>();
```

指定别名：

```ts
@Input('alias') propName = ...
```

2、在元数据中声明输入输出属性：

```ts
@Component({
  inputs: ['hero'],
  outputs: ['deleteRequest'],
})
```

指定别名：`'prop:alias'` 

```ts
@Component({
  inputs: ['hero:myHero'],
  outputs: ['clicks:myClick'],
})
```

**模板表达式操作符**：

- 管道操作符 (`|`) ：数据转换。

- 安全导航操作符 (`?.`) ：在属性路径中出现 null 和 undefined 值时，保护视图渲染器，让它免于失败。如 `{{nullHero?.name}}`。

- 非空断言操作符 (`!`) ：防止 TypeScript 报告属性可能为 null 或 undefined"的错误，不做严格测试。

- 类型转换函数 （`$any()`）：使用 `$any()` 将表达式转换为 any 类型。

### 生命周期钩子

每个组件都有一个被 Angular 管理的生命周期。Angular 提供了**生命周期钩子**，把这些关键生命时刻暴露出来，赋予你在它们发生时采取行动的能力。

1.`ngOnChanges()`：当 Angular (重新) 设置数据绑定输入属性时相应。

2.`ngOnInit()`：在 Angular 第一次显示数据绑定和设置指令/组件的输入属性之后，初始化指令/组件。在第一轮 `ngOnChanges()` 完成之后调用，只调用**一次**。

3.`ngDoCheck()`：检测，并在发生 Angular 无法或不愿意自己检测的变化时作出反应。在每个 Angular 变更检测周期中调用，`ngOnChanges()` 和 `ngOnInit()` 之后。

4.`ngAfterContentInit()`：当把内容投影进组件之后调用。第一次 `ngDoCheck()` 之后调用，只调用一次。

5.`ngAfterContentChecked()`：每次完成被投影组件内容的变更检测之后调用。`ngAfterContentInit()` 和每次 `ngDoCheck()` 之后调用

6.`ngAfterViewInit()`：初始化完组件视图及其子视图之后调用。

第一次 `ngAfterContentChecked()` 之后调用，只调用一次。

7.`ngAfterViewChecked()`：每次做完组件视图和子视图的变更检测之后调用。`ngAfterViewInit()` 和每次 `ngAfterContentChecked()` 之后调用。

8.`ngOnDestroy()`：当 Angular 每次销毁指令/组件之前调用并清扫。 在这儿反订阅可观察对象和分离事件处理器，以防内存泄漏。在 Angular 销毁指令/组件之前调用。

> 不要在组件的构造函数中获取数据，`ngOnInit()` 是组件获取初始数据的好地方。
>

### 组件交互

**通过输入型属性绑定把数据从父组件传到子组件**：

```ts
@Input() hero: Hero;
```

**通过 setter 拦截监听输入属性值的变化**：

```ts
@Input()
set name(name: string) {
  this._name = (name && name.trim()) || '<no name set>';
}
get name(): string { return this._name; }
```

**父组件监听子组件的事件**。

**父组件与子组件通过本地变量互动**：

在父组件模板中新建一个本地变量 (模板引用变量) 来代表子组件，利用这个变量读取子组件的属性和调用子组件的方法。

**父组件调用 `@ViewChild()`** ：

如果父组件的*类*需要读取子组件的属性值或调用子组件的方法，可以把子组件作为 *ViewChild*，**注入**到父组件里面。

**父组件与子组件通过服务通讯**：

父组件和它的子组件共享同一个服务，利用该服务*在家庭内部*实现双向通讯。

