# ydpt
内蒙古师范大学计算机科学技术学院
移动应用平台开发实验报告










实验名称：
       
专业：网络编程  
        
班级：15网络编程
       
学号：20151104704 

姓名：刘锦江
   
时间：2017.7.4









一、计算器软件开发
1.计算器图示


2.详细设计
2.1主模块
2.1.1定义变量
    var flg = 0
    var temp = ""
    var s : String=""

2.1.2获取数字和计算符号
@IBAction func one(_ sender: Any) {
        out.text = out.text! + "1"
           }
    @IBAction func xiaoshu(_ sender: Any) {
        out.text = out.text! + "."    }
    
       @IBAction func two(_ sender: Any) {
        out.text = out.text! + "2"
    }
    @IBAction func three(_ sender: Any) {
        out.text = out.text! + "3"
    }
    @IBAction func four(_ sender: Any) {
        out.text = out.text! + "4"
    }
    @IBAction func five(_ sender: Any) {
        out.text = out.text! + "5"
    }
    @IBAction func six(_ sender: Any) {
        out.text = out.text! + "6"
    }
    @IBAction func seven(_ sender: Any) {
        out.text = out.text! + "7"
    }
    @IBAction func eight(_ sender: Any) {
        out.text = out.text! + "8"
    }
    @IBAction func nine(_ sender: Any) {
        out.text = out.text! + "9"
    }
    @IBAction func zero(_ sender: Any) {
        out.text = out.text! + "0"
    }
    @IBAction func jia(_ sender: UIButton) {
        s = out.text!
        out.text=""
        flg = 1
    }
    @IBAction func jian(_ sender: UIButton) {
        s = out.text!
        out.text=""
        flg = 2
    }
    @IBAction func cheng(_ sender: UIButton) {
        s = out.text!
        out.text=""
        flg = 3
    }
        @IBAction func qinghcu(_ sender: UIButton) {
        out.text=""
    }
    @IBAction func chu(_ sender: UIButton) {
        s = out.text!
        out.text=""
        flg = 4
    }

2.1.4对数字进行加减乘除运算并得出结果
     @IBAction func value(_ sender: UIButton) {
        switch flg {
        case 1:
            var temp : Double
            temp = Double(s)! + Double(out.text!)!
            out.text = "\(temp)"
        case 2:
            var temp : Double
            temp = Double(s)! - Double(out.text!)!
            out.text = "\(temp)"
        case 3:
            var temp : Double
            temp = Double(s)! * Double(out.text!)!
            
            out.text = "\(temp)"
        case 4:
            if out.text != "0"
            {
                var temp : Double
                temp = Double(s)! / Double(out.text!)!
            out.text = "\(temp)"
            }
            else{
                out.text = "wrong"
            }
            
        default:
            out.text = out.text
            
        }
3.调试分析
3.1 程序运行出现的问题
按钮属性设置出错
除法运算除数为0时能运算
3.2调试步骤
重新检查设置每一个按钮的属性
为除法运算添加除数为0时报错的功能










二.羽毛球记分软件开发
1.运行程序界面展示


双方都得20分时


胜出
选取图片





程序主要代码：
1 定义变量
var z = 0
var x = 0
var i = 0
var t = 0
var r = 0
var a : Int = 0
var b : Int = 0
var dlg = 0
var flagA = 0
var flagB = 0
var q = 0
var w = 0
2 结束比赛，初始化所有数据
    @IBAction func finish(_ sender: UIButton) {
       z = 0
         x = 0
         i = 0
         t = 0
        ascore.text = ""
        bscore.text = ""
         dlg = 0
         flagA = 0
         flagB = 0
        score1.text = ""
        score2.text = ""
        firemsg.text = ""
        result.text = ""
        gamenum.text = ""
        q = 0
        w = 0
        fire1.text = ""
         fire2.text = ""
         fire3.text = ""
         fire4.text = ""
    
        
        
    }
羽毛球三局两胜制，现实当前是第几局，并在局数大于4时结束：
    @IBAction fund restart(_ sender: UIButton) {
        z = 0
        x = 0
        ascore.text = "\(0)"
        bscore.text = "\(0)"
        i = i+1
        gamenum.text = "第\(i)局"
        firemsg.text = ""
        result.text = ""
        if(i>=4){
            gamenum.text="结束"
        }
    }

3 上传选手照片
 @IBAction func Aput(_ sender: Any) {
        if dlg == 0{
        flagA = 1
        flagB = 0
        if UIImagePickerController.isSourceTypeAvailable(.photoLibrary)
        {
            let picker = UIImagePickerController()
            picker.delegate = self
            picker.sourceType = UIImagePickerControllerSourceType.photoLibrary
            self.present(picker,animated: true,completion: {
                ()->Void in
            })
        }else{
            print("读取相册错误")
            }
    }
    }
    
    @IBAction func Bput(_ sender: Any) {
        if dlg == 0{
            flagB = 1
            flagA = 0
            
            if UIImagePickerController.isSourceTypeAvailable(.photoLibrary)
            {
                let picker = UIImagePickerController()
                picker.delegate = self
                picker.sourceType = UIImagePickerControllerSourceType.photoLibrary
                self.present(picker,animated: true,completion: {
                    ()->Void in
                })
            }else{
                print("读取相册错误")
            }
        }

    }
添加照片函数：
    func imagePickerController(_ picker : UIImagePickerController,
                            didFinishPickingMediaWithInfo
        info:[String:Any]){
        print(info)
        let image : UIImage!
        image = info[UIImagePickerControllerOriginalImage]as!UIImage
        if(flagA == 1){
            Aimg.image = image
        }
        else if(flagB == 1){
            Bimg.image = image
        }
        
        picker.dismiss(animated:true,completion: {
            ()-> Void in
        })
    
    }
4 选手得分
@IBAction func addA(_ sender: UIButton) {
        q = x
        x = x + 1
        
        ascore.text = "\(x)"
        firemsg.text = “A选手发球"
／／羽毛球比赛规则，得分选手发球，信息框提示“a或b选手发球”
        
         if x % 2 == 0 {
         fire4.text = ""
         fire3.text = ""
         fire1.text = "F"
         fire2.text = ""
         }else{
         fire3.text = ""
         fire1.text = ""
         fire2.text = "F"
         fire4.text = ""
         }
／／得分者发球，如果得分为单数发球位置在左边，双数为右边，此代码为显示发球位置
       
        
        if x >= 21
        {
            if z >= 20,x - z == 2{
                result.text = "此局A选手胜"
                t = t + 1
                score1.text = "\(t)"
            }else if z <= 19{
                result.text = "此局A选手胜"
                t = t + 1
                score1.text = "\(t)"
            }
／／都得到20分时，连得两分者获胜
            if z == 29, x == 30{
                result.text = "此局A选手胜"
                t = t + 1
                score1.text = "\(t)"
            }
        }
／／都得29分时，先得一分者获胜
        if t == 2{
            result.text = "A选手胜出"
            z = 0
            x = 0
            ascore.text = "\(0)"
            bscore.text = "\(0)"
            i = 0
            t = 0
            r = 0
        }
        

    }
@IBAction func addB(_ sender: UIButton) {
        w = z
        z = z + 1
        bscore.text = "\(z)"
        firemsg.text = "B选手发球"
         if z % 2 == 0 {
         fire4.text = "F"
         fire3.text = ""
         fire1.text = ""
         fire2.text = ""
         }else{
         fire3.text = "F"
         fire1.text = ""
         fire2.text = ""
         fire4.text = ""
         }

        
        if z >= 21
            
        {
            if x >= 20,z - x == 2{
                result.text = "此局B选手胜"
                r = r + 1
                score2.text = "\(r)"
            }else if x <= 19{
                result.text = "此局B选手胜"
                r = r + 1
                score2.text = "\(r)"
            }
            if x == 29, z == 30{
                result.text = "此局B选手胜"
                r = r + 1
                score2.text = "\(r)"
            }
        }
        if r == 2{
            result.text = "B选手胜出"
            z = 0
            x = 0
            ascore.text = "\(0)"
            bscore.text = "\(0)"
            i = 0
            t = 0
            r = 0
        }

    }
5 撤销
   @IBAction func backA(_ sender: UIButton) {
        if x > q {
            ascore.text = "\(q)"
            x = q
            
        }
        if x % 2 == 0 {
            fire4.text = ""
            fire3.text = ""
            fire1.text = "F"
            fire2.text = ""
        }else{
            fire3.text = ""
            fire1.text = ""
            fire2.text = "F"
            fire4.text = ""
        }
       
    }
    @IBAction func backB(_ sender: UIButton) {
        if z > w{
            bscore.text = "\(w)"
            z = w
        }
        if z % 2 == 0 {
            fire4.text = "F"
            fire3.text = ""
            fire1.text = ""
            fire2.text = ""
        }else{
            fire3.text = "F"
            fire1.text = ""
            fire2.text = ""
            fire4.text = ""
        }

    }
    
调试分析
       根据羽毛球比赛规则，可实现三局两胜制，得分为20分，29分时获胜的方式，可以显示是谁发球，并显示他的位置，可以上传选手照片

 出现的问题：
难以实现选手发球位置随得分改变
按钮和文本框属性设置出错


调试步骤：
       添加四个位置的文本框，为每一次得分添加if语句，得分为双数和单数时显示“f”，其他文本框不显示

一一检查按钮属性，重新设置

  课程实验小结
       通过这次的实验我了解到了如何使用swift语言编程，不习惯使用x—code，通过在网上的学习和同学老师的帮助，渐渐入门，感觉到了用x—code这一简便编程工具的乐趣，并更对此产生了兴趣。

参考文献：
［1］百度 http://baidu.com
［2］SwiftV课堂—中国最大的Swift视频学习网站 http://www.swiftv.cn
