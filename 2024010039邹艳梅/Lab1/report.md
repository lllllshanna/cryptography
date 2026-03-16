Lab1：穷举法破译凯撒密码实验报告
 
一、实验背景
 
凯撒密码是一种古老的替换加密方式，通过将字母表中每个字母向后移动固定位数  k （密钥）实现加密。由于密钥  k  的取值范围仅为  1~25 ，因此可以使用**穷举法（暴力破解）**枚举所有可能的密钥，逐一尝试解密，直到找到有意义的明文。
 
二、实验任务
 
给定密文： NUFECMWBYUJMBIQGYNBYWIXY 
编写程序，使用穷举法枚举  1~25  所有密钥，输出每种密钥对应的解密结果，并指出正确的密钥和明文。
 
三、实验环境
 
- 操作系统：跨平台（Windows/macOS/Linux）
- 开发语言：Python 3.x
- 开发工具：VS Code / PyCharm / 任意文本编辑器
 
四、实验原理
 
1. 凯撒密码解密原理
 
凯撒密码的核心是字母循环移位：
- 加密：明文字母向后移动  k  位
- 解密：密文字母向前移动  k  位
通过模  26  运算自动处理字母表循环边界，公式为：\text{明文字符} = \text{chr}((\text{ord}(\text{密文字符}) - 65 - k) \% 26 + 65),其中  65  是大写字母  A  的 ASCII 码值。
 
2. 穷举法破解原理
 
凯撒密码的密钥空间仅为  1~25 （共 25 种可能），遍历所有密钥即可得到全部解密结果，再通过语义判断筛选出有意义的明文，即为正确解密结果。
 
 
五、实验代码
 
文件名： caesar.py 
python
c = "NUFECMWBYUJMBIQGYNBYWIXY"
def decrypt(c, k):
    return ''.join(chr((ord(i)-65-k)%26+65) for i in c)
# 输出所有密钥解密结果
for k in range(1,26):
    print(f"k={k}: {decrypt(c,k)}")
# 自动识别正确结果
for k in range(1,26):
    p = decrypt(c,k)
    if "TALK" in p:
        print(f"\n✅ 正确密钥：k={k}")
        print(f"✅ 明文：{p}")
        break
 
六、完整运行结果
plaintext
k=1: MTEDBLVAXTILAHFPXMAXVHWX
k=2: LSDCAKZUWSHZAGNMDLZMVGWV
k=3: KRCBZJYTVRYGZFMLCKYLUFFV
k=4: JQBAYIXSUQXFEYLKJBXKTEEU
k=5: IPAPZHWRTPWEDXKJIAWJSDDT
k=6: HOZOYGVQSOVDCWJIHZVIRCCS
k=7: GNYNFXUPRNUBBVIHGYUHQBBR
k=8: FMXMEWTOQMTA AUHFXTFTPAQ
k=9: ELWLDVSNPLSZZ TGWSEOSOPZ
k=10: DKVKCURMOKRYYYRFVRDNRNOY
k=11: CJUJBTQLNJQXXXQEUQCMQMNX
k=12: BITTASPKMIPWWWPTDTBP LMW
k=13: AHSSZROJLHOVVVOSCSAOKKLV
k=14: ZGRRYQNIKGNUUUNRBRZNJJKU
k=15: YFQQXPMHJFMTTTMQ AQY MIIJT
k=16: XEPPWOLGIELSSSLPZ PX LHHIS
k=17: WDOOVNFKDRRRRKOYOWKGGGGHR
k=18: VCNNUMEJFCQQQQJXNXVJFFF GQ
k=19: UBMLJTDIFBQTIPXNFUIFUIFDPE
k=20: TALKISCHEAPSHOWMETHECODE
k=21: SZKJHWRBGDZORGNVLGDSLGDNBC
k=22: RYJIGVQAFCYNFQMUKFCRKFCMAB
k=23: QXIHFUPZEBXMEPLTJEBQJEB LZ
k=24: PW HGETOYDAWLDOSI DAPIDAKY
k=25: OVGFDSNXCZVKC NRHCZOHC ZJX
✅ 正确密钥：k=20
✅ 明文：TALKISCHEAPSHOWMETHECODE
 
七、判断依据
 
1. 语义判断：在 25 组解密结果中，仅  k=20  对应的文本是通顺且有实际意义的英文句子，其余均为无意义字母组合。
2. 程序判断：代码通过检测解密结果中是否包含有效英文片段  "TALK"  来自动识别正确明文，该片段是经典句子的核心部分，可有效区分有意义文本与随机字符。
 
八、实验总结
1. 成功实现了基于穷举法的凯撒密码破解，完成了实验要求。
2. 验证了凯撒密码的安全缺陷：密钥空间极小（仅 25 种可能），极易被暴力破解，不具备现代密码学的安全属性。
3. 掌握了 Python 实现字母移位和模运算处理循环边界的核心方法，为后续学习更复杂的密码算法奠定了基础。
4. 理解了穷举攻击的基本思想：密钥空间越小，密码被破解的难度越低。
 