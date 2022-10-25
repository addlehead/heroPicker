#### 一、文件说明

- heroPicker
    - demo.go                       示例源程序文件
    - hero.go                       选将SDK源文件
    - heroes.txt                    将领编号文件
    - readme.md                     操作说明文档
    - LinuxDemo                     Linux环境下的执行文件
    - MacDemo                       Mac Intel芯片环境下的执行文件
	- MacM1Demo                     Mac M1芯片环境下的执行文件
    - Windows10Demo.exe             Windows10环境下的执行文件
	- Windows11Demo.exe             Windows10环境下的执行文件

#### 二、使用方法

+ 2.1 使用脚本命令行下执行，有3个参数需要注意：
```
-i 2022118											//表示手动输入双色球某一期的期号，将自动获取该期的开奖号码
-n 12,17,22,27,30,31,02					//表示手动输入某一期的开奖号码6红+1蓝
-s 1													//表示手动输入本期选将的起始序号
```

+ 2.2 原生Golang环境下执行: 进入文件目录heroPicker下运行: 
```
go run demo.go hero.go				//说明：如需带上相应的参数，则使用2.1中的对应参数及值
```

+ 2.3 Windows环境下系统版本7-10之间可以打开cmd，在cmd下进入文件目录heroPicker下运行:
```
 WindowsDemo.exe						//说明：如需带上相应的参数，则使用2.1中的对应参数及值
```

+ 2.4 Mac环境下: 进入文件目录heroPicker下运行:
```
 ./MacM1Demo									//说明：如需带上相应的参数，则使用2.1中的对应参数及值
 ./MacDemo										//说明：如需带上相应的参数，则使用2.1中的对应参数及值
```

+ 2.5 Linux环境下: 进入文件目录heroPicker下运行:
```
 ./LinuxDemo								//说明：如需带上相应的参数，则使用2.1中的对应参数及值
```

#### 三、武将发售规则说明

+ 3.1 双色球组合
	+ 3.1.1 双色球组合规则
```
双色球共有7个号码，以6红色球+1蓝色球形式排列。
其中红色球为1～33随机，蓝色球为1～16随机。
按照 A、B、C、D、E、F、G 依次填入
注意：该开奖号码的红球，已经是按照从低到高顺序排列，而不是出球顺序
```

+ 3.2 选将参数设置
	+ 3.2.1 根据这3.1中设置的7个双色球开奖号码，计算10个选将参数T1～T10，如下：
```
T1 = A+G
T2 = B+G
T3 = C+G
T4 = D+G
T5 = E+G
T6 = F+G
T7 = A+F
T8 = B+E
T9 = C+D
T10 = A+B+C
```
	+ 3.2.2 再从本期初始将领序号N开始，进行计数，得到10个武将序号N1～N10
```
N1 = N +T1
N2 = N1+T2
N3 = N2+T3
N4 = N3+T4
N5 = N4+T5
N6 = N5+T6
N7 = N6+T7
N8 = N7+T8
N9 = N8+T9
N10 = N9+T10
```
	+ 3.2.3 例如：从N，计数T1个，即获得N1。以此类推。
	+ 3.2.4 当序号计数结果超过可选将领最大序号时，从头循环计数;例如：计数达到序号50，再往下计数就是序号1。

+ 3.3 选将规则说明
	+ 3.3.1 常规阶段,第一次正式发售时，N=1。下一期抽取开始时，N=上一期N10。
	+ 3.3.2 序号轮空:轮空的武将，其序号在计数时，会被直接跳过；轮空的判定：
```
本期已经被抽取的武将，在后续计数时，其序号不再被抽取，设定为【轮空】
当某个序号的武将卡牌全部发行完毕时，其序号不再被抽取，设定为【轮空】。
```

+ 3.4 特别说明：
	+ 3.4.1 在发售后期，当大部分将领都已经发售完毕，剩余未发售将领总数不超过10个时，则无需抽取，剩余所有将领都被选中。

<br>
<br>




