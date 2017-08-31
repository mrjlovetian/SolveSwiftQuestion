# SolveSwiftQuestion
### 懒加载方法
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

### swift图片压缩的指定大小
```
func scaleImageImageUrl(imageUrl: String) -> NSData {
        
        var imageData: NSData?
        let url = URL(string: imageUrl)!
        imageData = NSData.init(contentsOf: url)
        let maxFileSize: Int = 31*1024;
        var compression: CGFloat = 0.9;
        let maxCompression: CGFloat = 0.02;
        var image = UIImage.init(named: "ico_waiting")
        if imageData != nil {
            image = UIImage.init(data: imageData! as Data)
        }
        
        var thumbImage = image
        let imageSize = CGSize(width: 200, height: (200.0*(image?.size.height)!)/(image?.size.width)!);
        if (image?.size.width)! > CGFloat(200.0)
        {
            UIGraphicsBeginImageContext(imageSize)
            let imageRect = CGRect(x: 0, y: 0, w: imageSize.width, h: imageSize.height)
            image?.draw(in: imageRect)
            thumbImage = UIGraphicsGetImageFromCurrentImageContext()
            UIGraphicsEndImageContext()
        }
        
        var compresseData = UIImageJPEGRepresentation(image!, compression)
        while compresseData!.count > maxFileSize && compression > maxCompression {
            compression -= 0.02
            compresseData = UIImageJPEGRepresentation(thumbImage!, compression)
        }
        return compresseData! as NSData
    }
```

## 颜色转换成图片
```
class func imageWithColor(color:UIColor) -> UIImage {
        
        let rect: CGRect = CGRect(x: 0, y: 0, width: 1, height: 1)
        UIGraphicsBeginImageContextWithOptions(CGSize(width:1, height:1), false, 0)
        color.setFill()
        UIRectFill(rect)
        let image: UIImage = UIGraphicsGetImageFromCurrentImageContext()!
        UIGraphicsEndImageContext()
        return image
    }
```

## 正确的隐藏导航栏底部的细线
```
public override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        
        self.navigationController?.navigationBar.setValue(true, forKey: "hidesShadow")
    }
```


