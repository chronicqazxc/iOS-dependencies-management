# iOS-dependencies-management
In this article I'll introduce some most popular 3rd dependencies management in iOS development according to my personal experience the useful tips as well as some pain points.   

|Tool|Description|Demo|
|--|--|--|
|**CocpaPods**|CocoaPods is popular iOS 3rd party management tool which provide lots of useful features like 1) Semanitic version control. 2) Modify prject configurations in hooks (pre_install, post_install). 3) Install pods according to configurations (Debug/Release/...) 4) Support multiple sources GitHub/GitLab/GitHub Enterprise as long as the framework support CocoaPods. According to personal experience if you have many pod dependencies the compile time would be impact since it will build every dependencies everytime you click `build` in Xcode (except the dependency is prebuild-framework). | [Podspec Demo](https://github.com/chronicqazxc/DemoPresenter) <br/> [Podfile Tricks]()|
|**Carthage**|Carthage is also popular in iOS development community, it is easy to use and use to adopt (become a Cartahge supported framework), since it will compile dependencies into frameworks so it is tricky to debug dependecies (if you are both  framework and base code provider) and it is easy to get stucked when you perform `carthage update` if the dependencies is too complicated, but we have solutions for above pain points. | [Tricks](/carthage_tricks.md) |
|**SwiftPackageManager**| SwiftPackageManager is Xcode native supported but it only support framework which wrote in Swift as well as doesn't support iOS projects. ||

Author: [Wayne Hsiao](chronicqazxc@gmail.com)
