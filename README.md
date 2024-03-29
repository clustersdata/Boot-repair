# Boot-repair
Boot-repair
谈谈谐振频率校正因子
1 频率校正因子的基本知识
通常理论计算的频率是谐振频率，由于忽视了非谐振效应，而且理论方法本身也有误差，所以直接基于它计算基频、零点能、焓、熵都可能有较大误差。而将频率校正因子（后文简称校正因子）乘在理论计算出的谐振频率上，基频以及热力学校正量就变得较为准确了，往往能减小2、3倍误差。例如一般杂化泛函算出的基频误差能到100多cm-1，而校正后一般只有几十cm-1的误差。由于忽略了非谐振效应会高估频率，因此基频的校正因子一般都小于1.0。

校正因子分为多种，通常有
(1)用于获得准确基频(fundamental)的校正因子。通常对于所有频率都是相同的校正值，但有些人为了校正得更准确，把频率划分成不同范围（比如高频和低频范围），分别给出不同的校正因子
(2)用于获得准确谐振频率的校正因子。注意谐振频率不是实验可观测的而只是个概念，但可以通过一定手段将实验数据转化得到
(3)用于获得准确的ZPE的校正因子
(4)用于获得准确的焓变ΔH=H(T)-H(0)的校正因子。注：H(0)=U(0)=电子能量+ZPE
(5)用于获得准确的熵的校正因子
这5种校正因子各不相同，不要随意混用。不过(1)/(3)以及(2)/(3)的数值对各种情况倒是基本总是固定的，分别为0.974和1.014。对HF或DFT，(4)和(5)的数值比较接近，混用也无妨。ΔH和熵的数值是依赖于计算时设定的温度的，其校正因子也因此受温度影响。

由于谐振子模型下ZPE是频率的线性函数，即ZPE=∑hν/2，所以第(3)类校正因子乘到原始频率上还是乘到基于原始频率算出的ZPE上效果都一样。但是对于(4)和(5)类校正因子，要分别乘到原始频率上再算ΔH和熵，而切不要用原始频率算完了之后再对所得的ΔH和S乘上校正因子。

还有一点要说明，由于ZPE=∑hν/2，表面上看仿佛只要对振动频率ν乘上校正因子成为准确基频后ZPE就应该准确了，因此(1)和(2)类校正因子仿佛应当是相同的，这是误解！因为这种ZPE的计算公式是对于谐振模型而言的，既然校正成了实际的非谐振频率，那么当然ZPE也得按照非谐振子来算才行。严格的非谐振的ZPE必须直接做非谐振计算才能得到。ZPE的校正因子则实际上是先乘到谐振频率上将之转化成一种特殊频率，然后再按照ZPE=∑hν/2来算的时候，得到的结果就能正好和实际的ZPE很接近。

2 频率校正因子的获取
校正因子一般都是用先人拟合好的，通过向相应类型实验数据拟合来得到。用于拟合的分子少则几种，多则上百种。常用的校正因子可以在这些地方得到：
1 http://comp.chem.umn.edu/freqscale/version3b2.htm。这是Truhlar组拟合的一大堆校正因子，相当全面，包括前述的(1)、(2)、(3)类校正因子。不过很遗憾的是没有给出ΔH和熵的校正因子。

2 http://cccbdb.nist.gov/vibscalejust.asp。这是Computational Chemistry Comparison and Benchmark DataBase(CCCBDB)数据库中的一页，给出的是基频的校正因子。

3 J. Phys. Chem., 100, 16502-16513 (1996)中的表10，给出的是前述(1)、(3)、(4)、(5)类校正因子。注意表10的ΔH和S的校正因子是298.15K下的，其它温度下的见文中图2。此文作者后来在2007年又发了一篇文章J. Phys. Chem. A, 111, 11683-11700 (2007)，给出了更多方法和基组（主要是pople基组）下的校正因子。

4 J. Phys. Chem. A, 108, 9213-9217 (2004)。给出的是HF、MP2和B3LYP结合Dunning相关一致性基组的各类校正因子。

5 J. Comp. Chem., 33, 2380 (2012)。给出了一些泛函结合pc系列基组的高频、低频、焓、熵、ZPE的校正因子。

6 Theor. Chem. Acc., 105, 413 (2001)。给出了HF、几种泛函和MP2结合Sadlej pVTZ基组时的高频和低频校正因子

网友Liyuanhe整理了一个很好的表格，汇总了各种来源（包括上述的）的校正因子，查阅方便，值得下载留存，见http://bbs.keinsci.com/forum.php?mod=viewthread&tid=3805。

虽然这些来源拟合校正因子过程所用的测试集和方法有异，但对于同种级别，结果是接近的，因此它们是有可比性的。还有一些校正因子零零碎碎地在一些文献中报道，用得较少，可靠性难说。

对于HF和各种GGA泛函，基频的校正因子分别接近0.9和1.0。这即是说GGA泛函由于理论方法误差和非谐振效应抵消，不做校正算出来的基频也挺准确。而HF由于显著高估力常数，所以算出来的频率太高，算出来的3000cm-1实际上只有约2700cm-1而已。杂化泛函的基频校正因子则介于0.9~1.0之间，而且数值和HF成分是近似呈线性反比关系的。

3 关于频率计算级别的选择
注意振动频率和热力学校正量的计算绝对不是用的理论级别越高越好。CCSD(T)/cc-pVTZ可能还不如B3LYP/6-31G*算出来的频率准确，因为误差既来自于理论方法给出的力常数的误差，也来自于忽略了非谐振效应的误差。在某些低水平下，可能恰好这两部分抵消得好，导致结果不错，GGA泛函算的基频几乎不需要校正就是这个原因。而如果盲目地用很高的计算级别，虽然基本消除了理论方法本身的误差，但非谐振效应缺乏较好的抵消，那么所得的基频以及热力学校正量很可能比很烂的级别算出来的还糟。另外还有关键的一点，就是在使用了校正因子后，不同方法间的差距会很大程度上拉平，原本差的方法在校正后结果可能很好。这正是为什么热力学组合方法G3，虽然目标是QCISD(T)的精度，却采用HF/6-31G*（经过校正因子校正）这样表面看上去如此烂的级别来算ZPE。所以说，用很高级别的方法去做振动分析是⑨的行为，何况计算二阶导数还那么费时，纯属白耽误功夫。半经验方法也有对应的校正因子，但是即便是经过校正后，误差还是较大，大于从头算方法很多，所以除非迫不得已不宜用半经验方法算频率。基于分子力场也可以算频率和热力学校正量，如果分子力场选得合适，那么结果可能很不错，且不需要做校正，例如MMFF94和MM3对于典型有机分子基频平均误差在60cm-1左右。

通常来说，使用B3LYP/6-31G*结合频率校正因子就能得到很好的计算结果，计算量小，而且比起其它多数方法（哪怕是更昂贵的）经过校正后的结果更好，所以完全不需要考虑其它的。虽然Truhlar的文章表明VSXC经过校正后更准确一点，但毕竟是相对小众向泛函，寡人不推荐。BMC-CCSD经过校正后特别准确，但毕竟比较贵，除非是要做高精度计算否则就不推荐了。

虽然频率校正因子校正后的B3LYP/6-31G*是通常推荐的做振动分析的级别，但是有些体系，可能在B3LYP/6-31G*下面优化的结果很糟，诸如弱相互作用显著的情况，进而可能由此导致算出的频率和热力学校正量都很差（即便已经经过校正）。此时就应该选择更合适的方法做振动分析以及对应的优化。例如对于弱相互作用对结构影响显著的时候可以用M06-2X、wB97XD。一个有点麻烦的问题是诸如M06-2X、wB97XD这样的稍微较新的泛函缺乏ΔH和熵的校正因子，不过从JPC,100,16502的数据来看，杂化泛函的这两类校正因子都比较接近于1.0，所以不做校正也没什么问题。另外，也可以在B3LYP优化和振动分析时加上DFT-D校正解决这个问题，看《乱谈DFT-D》（http://sobereva.com/83）、《DFT-D色散校正的使用》（http://sobereva.com/210）、《谈谈“计算时是否需要加DFT-D3色散校正？”》（http://sobereva.com/413）。

各类校正因子对于所用基组都不敏感（除非是和很小的基组相比），所以如果你用的基组没有对应的校正因子，可以直接用此方法在相近的基组下的校正因子。特别值得一提的是弥散函数对校正因子的影响微乎其微，所以假设你的基组用的是6-31+G*，但是找不到相应的校正因子，却能找到6-31G*下的校正因子，那么就可以放心地用6-31G*的校正因子。另外，对于同一种方法，无论是校正前还是校正后，都不代表越大的基组下结果越准确，而通常是差不多（除非基组烂到3-21G这种层次），因此根本没必要用双zeta以上的基组、带弥散函数做振动分析。经常有人问用混合基组时怎么选择校正因子，实际上此时没有完美的做法，一种做法是索性根本不考虑校正因子，还一种也有道理的做法是使用占原子数最多的基组的频率校正因子。而如果你只对某个振动频率感兴趣，而这个振动模式涉及的原子基本上用的都是基组A，那可以使用A基组对应的频率校正因子。

要提醒的是，振动分析所用的级别和优化几何结构的级别必须严格一致，而得到的热力学校正量是可以加到其它更高水平方法算的电子能量上的。比如说，要算一个体系某温度下的气相下的自由能，那么可以用B3LYP/6-31G*去优化体系然后在考虑校正因子的情况下做振动分析，得到ZPE、ΔH和熵，再用很好的方法诸如PWPB95-D3/def2-QZVP去获得这个结构下的电子能量E。最后体系的自由能G=E+ZPE+ΔH-T*S。

实际上，自行拟合频率校正因子不是难事，见《自行拟合基频校正因子与ZPE校正因子的简单方法》（http://sobereva.com/391），用自行拟合的显然比凑合借用一个更有信服力。

注意校正因子并非总能很好解决振动问题，尽管通常可以。用校正因子后只是整体统计结果变好了，并不代表对每种体系都能很好处理，比如很多级别下对于氟分子的振动频率算得都不咋样。并且对于非谐振效应很强、很低频率的情况，用了校正因子后结果肯定也还是不好，只能直接去做非谐振计算才行。更多相关讨论见《基频频率校正因子实际效果测试》（http://sobereva.com/390）。

4 在Gaussian中使用频率校正因子
下面简单说一下在Gaussian中使用校正因子的方式。在freq任务过程中使用scale=X就代表校正因子为X，例如
#P HF/6-31G* freq scale=0.9135 temperature=323
注意输出信息中只是在计算热力学校正量的时候对所用频率乘上了校正因子，而输出的频率还是原始的频率！所以要想得到校正后的频率，得自己手动把频率乘上校正因子。Gaussian显然是不会自动用校正因子的，即默认scale=1.0。

如果已经做过一次频率计算并且保存了chk文件，想查看另一个校正因子下的热力学数据，最好的方法是用Gaussian自带的freqchk工具，它会从chk文件中读取储存的Hessian矩阵并作分析。启动它之后，输入chk文件路径，然后依次输入
N    //不输出Hyperchem文件
323   //温度。如果输入0则为默认的298.15K
1     //压力。如果输入0则为默认的1atm
0.8905   //校正因子
[回车]
[回车]
然后立刻就看到了原始频率以及等同于scale=0.8905 temperature=323时freq任务给出的热力学数据，和Gaussian自身输出的一样。

利用freqchk，就可以反复利用不同校正因子得到较准确的ZPE、ΔH和熵，并获得自由能G=H-T*S，过程在下面说一下。以下是freq任务会输出的四个量，为了省事用字母表示，使用不同校正因子时它们都会有变化。
 Zero-point correction= A
 Thermal correction to Energy= B
 Thermal correction to Enthalpy= C   注意这一项不是ΔH，而是ZPE+ΔH
 Thermal correction to Gibbs Free Energy= D
首先，在ZPE校正因子下得到ZPE（即A）。然后在熵校正因子下得到-T*S（即D-C）。之后在ΔH校正因子下得到ΔH（即C-A）。最终将这三个量加在一起，再加上高精度方法算的电子能量E，就得到了自由能G=E+ZPE+ΔH-T*S。

在作IR、Raman、VCD这些振动光谱的谱图时，要先把频率乘上校正因子后再做图。手动一一去改Gaussian输出文件里的频率值显然太费事了。Multiwfn (http://sobereva.com/multiwfn)的绘制光谱图的功能可以方便地设定校正因子。启动Multiwfn后，载入Gaussian的freq任务的输出文件，选11进入光谱绘制功能，选IR或Raman，之后选0就可以显示光谱图。如果选14 Multiply the vibrational frequencies by a factor，就可以令不同编号范围的频率乘以指定的校正因子，重新作图后就能看到效果了。用户因此不仅可以对所有频率乘上统一的校正因子，还可以根据一些文章的思想，对于不同范围的频率乘上不同的校正因子以得到更准确结果。关于Multiwfn绘制光谱的更多信息看《使用Multiwfn绘制红外、拉曼、UV-Vis、ECD、VCD和ROA光谱图》（http://sobereva.com/224）。

最后顺带一提的是，除了对频率进行校正，还有人提出了直接对力常数进行校正的方法，不过这样的方法涉及到太多参数，难搞，所以没流行起来。对于NMR、UV/Vis等其它谱的计算也有人提出过不同级别下的各种校正方法，不过都远没有像频率校正因子这样被广泛使用。
