# MNK-Trigger
西内萌的6.0芒克触发器！
## 它可以做什么
- 告诉你下一个GCD打什么技能
## 它不可以做什么
- 告诉你oGCD技能怎么打，什么时候打
- 帮你摁键盘
- 帮你logs99
## 适用人群
- 想试试6.0新武僧但是又不想背循环的佛系玩家
## 如何使用
待施工
## 工作原理与局限
基于当前自身所处身形，buff/dot剩余时间，是否处于震脚状态，以及目前阴阳查克拉状态来判断下一GCD的最优选择
### 军体拳
> 当我们处于魔猿（1），盗龙（2），或猛豹（3）身形下时，每个GCD都是在二选一，因此我们根据是否需要补连击/buff/dot来决定打哪一个技能。

在正常情况下，本触发器提示的技能顺序与大家熟知的军体拳一致，即：
- 连击和双龙数量1:1
- 双掌和正拳数量1:1
- 破碎和崩拳数量1:2
### 震脚，红莲与必杀技
> 在6.0的武僧技改后，震脚，红莲与必杀技三者息息相关。简单来说，只有在开启震脚时能打必杀技，而必杀技是我们威力最高的技能，所以我们希望每一次必杀技都打进红莲里。而震脚40sCD，红莲60sCD，我们发现每奇数次的红莲内可以打2个必杀技，我们称为大红莲，而偶数次只能打出1个必杀技，我们称为小红莲。
> 我们又发现：
> - 1形下的技能平均威力最高
> - 阴必杀威力 < 阳必杀威力 < 真必杀威力
> - 我们每2次红莲都会使用3次必杀技
> 因此我们每2次红莲内使用必杀技的最优解为：**在不断buff/dot的情况下**打一阴一阳，真必杀使用1形技能触发（从技能释放的角度看等同于阴必杀）

#### 阴阳必杀技判断的优先级
本触发器会根据释放震脚时当前角色状态判断要使用阴必杀还是阳必杀，判断优先级由高到低为：
1. 不浪费阴阳查克拉
2. 不断dot/buff
3. 优先使用阴必杀

#### 大小红莲显示与调整
在木桩循环下，大小红莲会在每分钟交替。而在实战中，因为各种各样的原因会导致红莲的错位，如在奇数次红莲只打了一次必杀技。考虑到这种情况，本触发器提供了下一次红莲大/小显示，并会在每次红莲持续结束时更新。如果出现错位的情况，可以使用命令`/e !Reset RoF`进行调整。

#### Buff/Dot监视器



### 无相身形
> 由于必杀技命中后会给予我们无相身形
### 局限性
目前已知有以下问题：
1. 由于破碎拳dot生效时间与技能释放时间之间有延迟，会导致在使用破碎拳的这个GCD内开启震脚时阴阳必杀判断出错。建议使用上文提到的buff/dot checker来判断。
2. 由于必杀技未命中目标时不会给予玩家无相身形，会导致这一GCD插件不提示。建议，额，别空大。
3. 在打阳必杀时不会调整身形顺序，也不会重新选择起始身形。即如果开启震脚前的GCD我们打了1，那么接下来这三个GCD依旧会按照2-3-1的顺序触发阳必杀，而不会选择1-3-2，即使后者的威力更高。~~大概吧主要是为了这点威力多写很多判断实在太麻烦了(｀・ω・´)~~
4. 本触发器未考虑双阳起手。~~也是因为太麻烦了~~
## 鸣谢
