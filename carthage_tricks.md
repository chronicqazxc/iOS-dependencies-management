# Resolve the pain point of Carthage

## Complicated dependencies hierarchy
Imagine you are developing a huge project which has over 50+ dependencies (Despite this is bad for app cold launch speed but we don't discuss in here.) the hierarchy also very deep like the following diagram.
![](/.assets/carthage_dependencies.png)
We should treat the version for each dependencies very carfully or we will encounter version conflict when `carthage update`.

## Semanitic Version (Solution 1)
This is the commonly approach to deal with this scenario, but we have to build all frameworks as binary and release on GitHub.
*BaseApp/Cartfile*
```ruby
git "https://xxx.business-model-a.git" ~> 3.1.0
git "https://xxx.business-model-b.git" ~> 2.1.0
```

## Manage in BaseApp (Solution 2)
Since the final product we provided is BaseApp so we'd like to manage all the version of dependencies in our BaseApp. In order to achive that we have to complete folloinwg tasks.
1. Write all dependencies with specific versions in `Cartfile` for instance as following.   
*BaseApp/Cartfile*
```ruby
git "https://xxx.core.git" "1.2.1"
git "https://xxx.base-ui.git" "2.1.0"
git "https://xxx.service.git" "1.1.0"
git "https://xxx.profile.git" "1.0.0"
git "https://xxx.business-model-a.git" "3.1.0"
git "https://xxx.business-model-b.git" "2.1.0"
```
2. Prepare two **Cartfiles** for each frameworks which has dependencies.
For instance BusinessModelA
### Inside Cartfile (for Demo app)
*BusinessModelA/Example/Cartfile*
```ruby
git "https://xxx.base-ui.git" "2.1.0"
git "https://xxx.service.git" "1.1.0"
git "https://xxx.profile.git" "1.0.0"
```
### Outside Cartfile (for dependent)
*BusinessModelA/Cartfile*
```ruby
git "https://xxx.base-ui.git"
git "https://xxx.service.git"
git "https://xxx.profile.git"
```
The concept is when dependent (BaseApp) fetch the dependencies, Carthage will reference the Cartfile under the root folder of the framework and to analyse the necessary dependencies of the framework, since we don't specify the exact version of the dependencies, the Carthage will adopt the veriosn of Cartfile of dependent (BaseApp).
The key point here is we **MUST** perform `carthage update` with parameter `--new-resolver` for **BaseApp** e.g. `carthage update --new-resolver`.

## Conclusion
Both of these two solutions are available and working, only you need is to choose which approach is the most fit for your organization/team.

Author: [Wayne Hsiao](chronicqazxc@gmail.com)
