# SolveSwiftQuestion
###懒加载方法
```
lazy fileprivate var customerImageView:UIImageView = {
        () -> UIImageView in
        let temView = UIImageView()
        temView.frame = CGRect(x: 15, y: 2, w: 60 * RateW(), h: 60 * RateW())
        temView.layer.cornerRadius = temView.tt_height/2.0
        temView.clipsToBounds = true
        temView.backgroundColor = .blue
        return temView
    }()
```

### 屏幕缩放比例
```
/// - Returns: 与ip6屏幕对比之后的缩放大小(宽度)
func RateW() -> CGFloat{
    return (ScreenW/375)
}
```

