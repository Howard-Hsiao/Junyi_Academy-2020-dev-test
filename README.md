### 均一平台教育基金會平台發展組遠端筆試
<p>申請者：蕭昀豪</p>
<p>測驗時間限制：共 45 分鐘</p>
<p>開始時間　　：8/23 7:30</p>
<p>結束時間　　：8/23 8:15</p>
<p>花費時間　　：共 45 分鐘</p>

#### 1 
* (A) 請寫一個程式把裡面的字串反過來。
* (B) 請寫一個程式把裡面的字串，每個單字本身做反轉，但是單字的順序不變。
* (加分題) 請為你的程式寫 unit test。


```python
def reverseA(inputStr:str):
    if(not isinstance(inputStr, str)):
        raise TypeError("[!] Your input should be string. ")
        
    return inputStr[::-1]

def reverseB(inputStr:str):
    if(not isinstance(inputStr, str)):
        raise TypeError("[!] Your input should be string. ")
        
    strList = inputStr.split()
    strList = [i[::-1] for i in strList]
    strList = " ".join(strList)
    
    return strList
```


```python
import unittest

class TestReverseMethods(unittest.TestCase):
    
    def setUp(self):
        self.testStr = "flipped class room is important"
    
    def test_reverseA(self):
        expected = "tnatropmi si moor ssalc deppilf"
        self.assertEqual(reverseA(self.testStr), expected)

    def test_reverseB(self):
        expected = "deppilf ssalc moor si tnatropmi"
        self.assertEqual(reverseB(self.testStr), expected)

    def test_typeError(self):
        self.assertRaises(TypeError, reverseA, 0)
        self.assertRaises(TypeError, reverseB, 0)
        
if __name__ == '__main__':
    # the argument of unittest.manin is to enable unittest to be used in jupyter notebook
    unittest.main(argv=['first-arg-is-ignored'], exit=False)
```

    ........
    ----------------------------------------------------------------------
    Ran 8 tests in 0.005s
    
    OK
    

#### 2
* 請寫一個程式，Input 是一個數字，Output 是從 1 到這個數字，扣除掉所有 3 的倍
數以及 5 的倍數，但是需要保留同時是 3 和 5 的倍數的總數字數。
* (加分題) 請為你的程式寫 unit test。


```python
def specialNum(inputNum):
    if(not (isinstance(inputNum, int) or isinstance(inputNum, float))):
        raise TypeError("[!] Your input should be a number. ")
    if isinstance(inputNum, float):
        if(int(inputNum) != inputNum):
            raise TypeError("[!] You number should be an integer. ")
        inputNum = int(inputNum)
    
    intersect = int(inputNum // 15)
    three_num = int(inputNum // 3)
    five_num = int(inputNum // 5)    
    return inputNum - three_num - five_num + 2 * intersect
```


```python
class TestSpecialNum(unittest.TestCase):
    
    def setUp(self):
        self.testNum = 15
    
    def test_specitalNum(self):
        self.assertEqual(specialNum(self.testNum), 9)
        
    def test_typeError(self):
        self.assertRaises(TypeError, specialNum, "test")
        self.assertRaises(TypeError, specialNum, 15.5)
        
if __name__ == '__main__':
    # the argument of unittest.manin is to enable unittest to be used in jupyter notebook
    unittest.main(argv=['first-arg-is-ignored'], exit=False)
```

    ........
    ----------------------------------------------------------------------
    Ran 8 tests in 0.005s
    
    OK
    

#### 3
房間裡有三個袋子，一個只裝鉛筆，一個只裝原子筆，第三個有鉛筆也有原子筆。
袋子是不透明的，單從袋子的外表上看不出任何差異，你不知道哪個袋子裝什麼。
除了袋子上各貼了一個標示（"鉛筆"、"原子筆"、"混和"），且標示都是錯的
（e.g. 標示鉛筆的袋子可能是混和的或是只裝原子筆）。
你只能選一個袋子，拿出裡面一支筆，看是鉛筆還是原子筆，然後你要推論出這三
個袋子分別的情況。請列出你的作法，以及解釋為什麼這樣可以找到答案。

#### 答案:
從"混合"標籤的袋子拿出一枝筆來就可以確定3個袋子的內容物。在抽取前，3個袋子內容物只可能如下: 

標籤　: 真實內容物可能值
* 混和　: [鉛筆, 原子筆]
* 鉛筆　: [混合, 原子筆]
* 原子筆: [混合, 鉛筆]

從混合標籤袋取物有2種情況，在此我們舉「抽到物品為鉛筆」為例，當在混合標籤袋中抽到鉛筆，代表混合標籤袋裝的真面目其實是鉛筆袋，此時原子筆標籤袋可以經由刪去法推出它其實是混合袋，接著再經由刪去法，我們可以確認最後剩下的鉛筆標籤袋，一定是原子筆袋。
當在混合標籤袋「抽到原子筆」時，我們也可以經由相同思考邏輯判斷出每一袋的真實內容物

#### 4. 
有三個人一起到迪士尼遊玩，中午肚子餓了，去餐廳點了一份現在最夯的冰雪奇緣
雙人組，要價 900 元，付錢後，服務生發現今天套餐大特價，只要 750 元，因此
服務生應該退還 150 元給這三個人，但是這位服務生一時鬼迷心竅，決定暗槓 60
元，只退了 90 元給這三個遊客。
那麼：三人各出 300 元 - 服務生還給他們一人 30 元 = 三人各出 270 元。270
元 × 3 人+ 服務生私吞的 60 元 = 810 + 60 = 870 !? 怎麼不是 900 元呢？還
有 30 元去哪了呢？請用敘述的方式，儘量清楚解釋問題出在哪裡。

#### 答案
本題唯一的鐵則是收支平衡，我們用此概念去審視題幹即可發現盲點。
* 若無特價
    * 支: 300元是原先每人應付的錢。
    * 收: 300元是原先應對每人收取的金額。

* 在題意下
    * 支: 270元是原先每人實際付出的錢
    * 收: 20元是服務生對每人收的錢
    * 收: 250是餐廳實際收到的錢

在上述情境下，以此觀點思考都可得出收支平衡的結果。原先題幹的計算方式之所以有誤，原因在於題目試圖用「支 + 收 = 原價」去確認結果，然而「支 + 收」的計算結果不具意義，因此此方法錯誤。應該要用「支 + 服務生退款的錢 = 原價」公式計算才正確。以總價觀點來看，公式為「支(\$810) + 服務生退款的錢(\$90) = 原價(\$900)」
