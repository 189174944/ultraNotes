cocoapod更新

sudo gem install cocoapods -n /usr/local/bin

问题:LibreSSL SSL_read: SSL_ERROR_SYSCALL, errno 60 

解决方案:pod repo update

> ```objective-c
> BOOL isDark = (self.traitCollection.userInterfaceStyle == UIUserInterfaceStyleDark);
> ```



>
>
>```swift
>func loadXib() ->UIView {
>        let className = type(of: self)
>        let bundle = Bundle(for: className)
>        let name = NSStringFromClass(className).components(separatedBy: ".").last
>        let nib = UINib(nibName: name!, bundle: bundle)
>        let view = nib.instantiate(withOwner: self, options: nil).first as! UIView
>        return view
>    }
>```
>
>