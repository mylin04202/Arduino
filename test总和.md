```

```





# Session 1: Sound Part One

## Oscillation/振荡的定义

- Fundamental basis of all periodic phenomena
- Not just useful for sounds, but also images
- `sin(x)` function creates a sine wave
- This is a wave, or waveform
- `maxiOsc` object

## Air moving

- Wave goes above 0. --> Speaker moves forward
- Wave goes below 0. --> Speaker moves backward
- when the value of the wave is over 1 or below -1, you're in distortion
- i.e. the speaker can't move any further, so the waveform is clipped.

*The position of the speaker is the PHASE of the wave.*

## All about time

- Both sound and video are time based
- Interesting fusion occurs around 20Hz
- Getting things to happen at the right time is an important computational problem

## Frequency

Waves don’t just have a phase. They also have *frequency*

- This is how often they move up and down each second - measured in hertz (hz) (also called 'Cycles Per Second (cps)').
- Waves that oscillate more than around 20 times per second take on a quality of continuos sounds, and not separate pulses
- Interestingly, the same is roughly true for images (fps)
- Oscillations below 20hz are called “Low Frequency” (LFOs)

## Frequency 2

- It's generally considered that humans can't hear oscillations with freqencies over 20000hz (20KHz)
- This very often changes with age, reducing as hearing definition decreases (as hair cells in the Cochlea cease to function).
- It order to digitally represent any periodic oscillation, we need to take **at least** two measurements, or 'samples' (one for each peak phase position).
- This is why your digital audio system is considered most effective if it has a samplerate of at least twice the maximum frequency you can hear (e.g. 44100hz, 48000hz etc.)
- The samplerate is the number of times per second that your system can measure (record) or reproduce (play back) the amplitude value of a signal
- The maximum frequency your system can reproduce is half the samplerate, called the *Nyquist Frequency*. The samplerate is also equal to the *Nyquist Rate*, which everybody finds confusing.
- Remember - **the rate is twice the frequency**, even when it's the Nyquist rate. But the rate is **never** the Nyquist Frequency
- You should probably check the samplerate of your audio hardware when programming audio systems, and make sure you at least know what it is. It will cause you problems if you forget that it exists.
- 通常认为人类听不到频率超过20000hz（20KHz）的振荡
- 这通常随年龄而变化，随着听力清晰度的降低而降低（因为耳蜗中的毛细胞停止功能）。
- 为了数字化表示任何周期性振荡，我们需要**至少进行**两次测量或“采样”（每个峰值相位位置一个）。
- 这就是为什么您的数字音频系统的采样率至少是您可以听到的最大频率的两倍（例如44100hz，48000hz等）被认为是最有效的原因
- 采样率是系统每秒可以测量（记录）或再现（播放）信号幅度值的次数。
- 系统可以重现的最大频率是采样率的一半，称为*奈奎斯特频率*。采样率也等于*奈奎斯特率*，每个人都会感到困惑。
- 请记住-**速率是频率的两倍**，即使是奈奎斯特速率也是如此。但是速率**永远不会**是奈奎斯特频率
- 对音频系统进行编程时，您可能应该检查音频硬件的采样率，并确保至少了解它的含义。如果您忘记了它的存在，将会给您带来麻烦。

## Amplitude

Waves also have an amplitude.

- This is how much they move up and down.
- In the real world, this is how much air they are moving.
- The speaker reproduces this process based on the computer's representation
- Remember, when the amplitude value of the wave is over 1 or below -1, you're in distortion
- In the computer, we have a different situation in that it can be more, and we can clip on purpose, for example to change the nature of the wave.
- 这就是它们上下移动的程度。
- 在现实世界中，这就是他们正在移动的空气量。
- 演讲者根据计算机的表示重现此过程
- 请记住，当波的振幅值大于1或小于-1时，您处于失真状态
- 在计算机中，我们的处境不同，它可能会更多，而且我们可以有目的地进行限制，例如更改波的性质。

## Amplitude 2

- When we take a measurement of an oscillation (a sample), we store the value of the sample using a number of bits.
- 8 bit gives you a potential 256 values to represent the amplitude. This isn't great (although I like it).
- Most people agree that 16 bits per sample is fine. This gives you 65,536 numbers with which to encode a floating point value between 1 and -1.
- Many modern audio systems have much higher bitrates and sample rates.
- Reducing the bitrate is lots of fun and you should try it. You can use quantisation for this which is pretty simple to do by accident.
- 当我们测量振动（样本）时，我们使用许多位来存储样本的值。
- 8位为您提供了一个潜在的256个值来表示幅度。这不是很好（尽管我喜欢）。
- 大多数人都同意每个样本16位就可以了。这将为您提供65,536个数字，用于编码介于1和-1之间的浮点值。
- 许多现代音频系统具有更高的比特率和采样率。
- 降低比特率很有趣，您应该尝试一下。您可以为此使用量化，这很容易偶然发生。

## Adding sounds together

- In the computer, the audio output should vary between -1 and 1
- This is a linear measurement, not in dB - i.e. not logarithmic
- `dB = Math.log10(linear_volume)*10`, which means linear val 1 == 0dB, 0.5 = -3.010. It's times 10 because a deciBel is a tenth of a Bel.
- Let me know if you want me to bore your pants off about this.
- When you add sounds, they combine linearly and can create distortion
- At maximum, `1+1=2` ...which will cause clipping
- 在计算机中，音频输出应在-1和1之间变化
- 这是线性测量，不以dB为单位-即非对数
- `dB = Math.log10(linear_volume)*10`，这意味着线性val 1 == 0dB，0.5 = -3.010。它的倍数是10，因为分贝是Bel的十分之一。
- 让我知道您是否要为此烦恼。
- 添加声音时，它们会线性结合并产生失真
- 最多`1+1=2`...会导致削波

## Combining sounds in different ways

- When we add sounds together, strange things happen
- The sounds interfere with each other
  - Beating
  - Amplitude modulation - (multiplication)
  - Frequency modulation - (controlling frequency with another oscillator)

## Beating

- When two sinewave oscillators of different frequencies are added together, they interact to alter the amplitude
- This is because they cycle across each other. Sometimes, one will be at -1, while the other is at 1
- So the result becomes 0 at these points
- What you hear is the sound fading in and out.
- We call this 'beating'
- The beat frequency (how often it fades in and out) is equal to the difference between the two input frequencies.
- 当两个不同频率的正弦波振荡器加在一起时，它们会相互作用以改变幅度
- 这是因为它们彼此循环。有时，一个为-1，另一个为1
- 所以结果在这些点变成0
- 您所听到的是声音的淡入和淡出。
- 我们称此为“跳动”
- 拍频（淡入和淡出的频率）等于两个输入频率之差。

##  

## Amplitude Modulation

- A common example of amplitude modulation (AM) is when we multiply two sinusoidal oscillators together
- The output is two signals whose frequencies are the sum and the difference of the two input frequencies
- So if you multiply two sine waves together with frequencies of 400hz & 500hz, you will instead hear 900hz and 100hz
- 振幅调制（AM）的一个常见示例是将两个正弦振荡器相乘
- 输出是两个信号，其频率为两个输入频率的和与差
- 因此，如果将两个正弦波与400hz和500hz的频率相乘，您将听到900hz和100hz

##  

## Frequency Modulation 1

- We can use the output of a sinewave oscillator to control the frequency of another
- We do this by setting the frequency of the carrier oscillator, and adding the output of the second oscillator (the modulator) to it.
- If we don't change the amplitude of the modulator, not much will happen, because it will simply be adding a value between 1 and -1
- When we increase the amplitude of the modulator (i.e. change the 'modulation index'), this doesn't change the amplitude of the carrier - the sound output doesn't get louder
- Instead, the frequency of the sound changes in predictable, but nonetheless, very exciting ways
- 我们可以使用正弦波振荡器的输出来控制另一个振荡器的频率
- 为此，我们需要设置载波振荡器的频率，然后将第二个振荡器（调制器）的输出相加。
- 如果我们不改变调制器的幅度，则不会发生太大的事情，因为它将简单地添加一个介于1和-1之间的值
- 当我们增加调制器的幅度时（即更改“调制指数”），这不会改变载波的幅度-声音输出不会变大
- 相反，声音的频率以可预测的方式变化，但是仍然非常令人兴奋

## Frequency Modulation 2

- If the frequency of the modulator is greater than the threshold of pitch perception (20 hz), increasing the modulation index makes the sound brighter
- **i.e. the frequency content of the signal increases in complexity as you increase the modulation index**
- The higher the modulation index, the more sidebands are created, increasing the brightness of the sound
- If the carrier and modulator are factors or multiples of each other, there is less beating (the sounds are harmonics of one another).
- If not, there is increased beating (the sounds are inharmonic) and eventually, noise (they become highly complex).
- You can use this technique to do lots of things, including generating pseudo-random numbers.
- John Chowning demonstrated that you could theoretically use this technique to simulate almost any sound with enough parameterised modulators.
- 如果调制器的频率大于音高感知的阈值（20 hz），则增加调制指数会使声音更明亮
- **即，信号的频率含量随着调制指数的增加而复杂度增加**
- 调制指数越高，创建的边带越多，从而增加声音的亮度
- 如果载波和调制器是彼此的因数或倍数，则跳动更少（声音是彼此的谐波）。
- 如果不是这样，则会增加跳动（声音不和谐），并最终产生噪音（声音变得非常复杂）。
- 您可以使用此技术来做很多事情，包括生成伪随机数。
- John Chowning证明，理论上您可以使用这种技术来模拟具有足够参数化调制器的几乎所有声音。

<Frequency Modulation example>

- https://ccrma.stanford.edu/people/john-chowning
- https://ccrma.stanford.edu/sites/default/files/user/jc/fm_synthesispaper-2.pdf

# Session #1 Homework

Make sure you're familiar with how the MIMIC platform works.

Make sure you have created an account on the MIMIC platform.

Make a fork of this document if you want the simplest possible starting example :

https://mimicproject.com/code/8e5728dd-2eb9-02a9-9cb8-63d3731bba68

Or if you want to use the visualisation, use this one.

https://mimicproject.com/code/69704316-d8d8-7623-f0c6-316cb983f0b9

Use either as a basis for carrying out the following tasks:

- Using at least 4 oscillators, create a continuous, drone-based sound texture or sound bed.
- Use two of the oscillators to control parameters of the other two oscillators.
- Make the sound texture vary continuously over a period of 1 minute through the use of low-frequency oscillators, so that the sound texture develops over the entire period.

Further reading:

- Follow Chris Kiefer's tutorial on the Mimic platform: https://mimicproject.com/guides/maximJS
- Read this useful article from izotope on bit resolution and sampling rate -- https://www.izotope.com/en/learn/digital-audio-basics-sample-rate-and-bit-depth.htm

# Session 2: Sound Part Two



### Properties of Periodic Waves//周期波的性质

[![Wikimedia Commons Graph of a Sine Wave](https://camo.githubusercontent.com/99abbbcf370ad314759d2f56502f66ce2d863a5afe16cb48f06605de9340227b/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f312f31322f4669677572652d73696e652d67726170682d77696e73746f6e2e706e67)](https://camo.githubusercontent.com/99abbbcf370ad314759d2f56502f66ce2d863a5afe16cb48f06605de9340227b/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f312f31322f4669677572652d73696e652d67726170682d77696e73746f6e2e706e67)

- basic periodic signals（they have **Phase, Frequency and Amplitude**）
- **Phase** (what point the wave is in its periodic cycle). This is often measured in degrees (`0-360`) or radians (`0 - 2*PI`), or also by a point in time if the frequency is known. With a sine waveform, 0 degrees is the start, 90 degrees is the postive peak, 180 degrees is when it returns to the centre line, 270 degrees is the negative peak, and 360 degrees is the start of the next cycle. When we reach 360 (`2*PI`), we can either begin from 0 again (i.e., we can 'wrap' the phase so it's always between 0 and 360), or we can continue to increase the phase. **Mathematical functions for creating waves generally take inputs in radians**. Therefore, a waveform's phase at any time can be described by its position in time (as in the above diagram), or in radians / degrees, or by its real value.
- **Frequency** (how often they repeat their cycles). This is measured in Hertz (Hz), or CPS (cycles per second). Some people find this is a lot easier to think about than phase.
- **Amplitude** (the *absolute peak* output, the **maximum amount the speaker can move**). Amplitude is between 1 and -1, with a *node* when it *crosses zero*. By *absolute*, we mean with the sign removed, so -1 in that case can be thought of as 1 in absolute terms, despite needing to be considered as -1 for the purposes of representing the phase of the signal either side of 0.
- **相位**（波在其周期性周期中指向的点）。通常以度（`0-360`）或弧度（`0 - 2*PI`）为单位进行测量，如果已知频率，也可以按时间点进行测量。对于正弦波形，开始时为0度，正峰值为90度，返回中心线时为180度，负峰为270度，下一个周期的开始为360度。当我们达到360（`2*PI`）时，我们可以再次从0开始（即，我们可以“包装”相位，使其始终在0到360之间），或者我们可以继续增加相位。**用于产生波的数学函数通常以弧度作为输入**。因此，波形在任何时候的相位都可以通过其时间位置（如上图所示），弧度/度或它的实际值来描述。
- **频率**（他们多久重复一次周期）。单位为赫兹（Hz）或CPS（每秒周期）。有些人认为这比阶段容易得多。
- **振幅**（*绝对峰值*输出，**扬声器可以移动**的**最大量**）。振幅在1到-1之间，当它过*零时*会有一个*节点*。通过*绝对的*，我们指的是与标志去掉，这样-1在这种情况下，可以，认为在绝对数量为1，尽管需要被视为-1代表0的信号两边的相位的目的。
- *Both Amplitude and Frequency relate to Phase*
- Amplitude is the highest value the signal can produce (at its peak - remember, it's an oscillation through positive and negative phase!)
- Frequency is how often the complete phase cycle repeats every second
- The higher the frequency, the higher the perceived pitch
- The higher the overall amplitude, the higher the perceived volume
- *振幅和频率都与相位有关*
- 振幅是信号可以产生的最大值（在峰值处-请记住，它是正负相位之间的振荡！）
- 频率是整个相位周期每秒重复的频率
- 频率越高，音高越高
- 总振幅越高，感知到的音量越高
- **In addition, I provided you with some notes about how we record and represent these periodic signals in a computer. They mention the Nyquist rate, The Nyquist frequency, the sampling rate, and how this relates to the frequency response of the human hearing system. I also introduced the idea of data representation in the context of bit resolution, and how this relates to amplitude**

*Also*

### Complex Interactions Generated by Periodic Waves

- We learned how to add periodic signals together, how this can cause distortion, and also generate *beating*.

- We learned how to multiply them together to create *Amplitude Modulation* **(AM)**, and how this creates *sum and difference tones*.

- We learned how to use one periodic signal to control the frequency of another, and how how this creates *Frequency Modulation* **(FM)**

-  create complexity by doing this; for example, increasing the **modulation index** of the modulating wave (i.e., its local amplitude) increases the number of overtones (without generating distortion, as the main output doesn't change - remember, we're only changing the frequency). We perceive this as an increase in *brightness*. Also, when the frequencies are factors or multiples of one another, or some other value, we get harmonic overtones (less beating **because the nodes are in phase**), and if they aren't, we get more beating (**because the nodes are out of phase**)

- 通过这样做来创造复杂性；例如，增加调制波的调制指数（即它的局部振幅）会增加泛音的数量（不会产生失真，因为主输出不会改变--记住，我们只是改变了频率）。我们将其感知为亮度的增加。另外，当频率是彼此的系数或倍数，或其他一些值时，我们会得到谐波泛音（因为节点是相位的，所以跳动较少），如果不是，我们会得到更多的跳动（因为节点是不相位的）。

  

- We used variables, objects and basic functions. We also used basic operators (+, -, *, /)

- Some of you might have come across some additional math objects (abs, exp, sin, cos). I definitely used one of these which you will have seen if you were paying close attention.

- As promised, we're also going to look at some spectral plots so we can examine the way the signals interact in more detail:



example：voice modulation

Lets do this now: https://mimicproject.com/code/b6a1bbfa-5992-4e14-3814-0197d5984028



# Session 2: SAMPLES!

## What is a sample?//什么是样本？

- an individual value, or number, between -1 and 1, where the individual value (the *sample*) was usually stored in at least 16 bits. When you string these together, you get sound. These don't have to be simple sine waves. They can be any sound. Here's an example of some JavaScript arrays with sounds in them. These are 16 bit floating point values between -1. and 1., recorded 44,100 times per second.

https://www.doc.gold.ac.uk/~mus02mg/samples.js

- If you run all these values through a speaker at a rate which is the same as the rate they were recorded, you get a pretty good reproduction of the sound they represent. If you run the values through a speaker at a higher rate, the sound is faster and higher pitched, and if you do it more slowly, the sound is slower and lower pitched (there are some problems that occur when you do this that I'm going to talk about later)
- If you graphed one of these lists of numbers (e.g. just plotted them) you would see the entire waveform for that sound
- As we've already discussed, all sounds can be seen as a collection of sinusoidal waves added together. When they are added, they become a single waveform with lots of different frequencies interacting in complex ways.
- This isn't something you can just understand immediately. It takes time. But you should probably spend some time thinking very hard about it.
- **In any case, it's quite common for people to describe a selection of recorded samples as a 'sample', as well as to describe an individual amplitude value within a sample as a 'sample'. Both uses are correct**
- 介于-1和1之间的单个值或数字，其中单个值（*样本*）通常以至少16位存储。将它们串在一起时，会发出声音。这些不一定是简单的正弦波。它们可以是任何声音。这是一些带有声音的JavaScript数组的示例。这些是-1之间的16位浮点值。和1.，每秒记录44,100次。

https://www.doc.gold.ac.uk/~mus02mg/samples.js

- 如果通过扬声器以与所记录的速率相同的速率运行所有这些值，则可以很好地再现它们所代表的声音。如果您以较高的速率通过扬声器运行这些值，则声音会更快，音调更高；如果您做得更慢，则声音的音调会更低，音调更低（这样做时会出现一些问题，我稍后再说）
- 如果您绘制了这些数字列表之一（例如刚刚绘制了它们），您将看到该声音的整个波形
- 随意在excel中执行此操作。您可能需要将这些值复制并粘贴到文本文件中，然后将其作为逗号分隔值（.csv）导入，确保选择逗号作为分隔符，这实际上应该很明显，但是对于excel并不是很不幸，所以要当心。
- 正如我们已经讨论过的，所有声音都可以看作是正弦波加在一起的集合。添加它们后，它们将变成具有许多不同频率以复杂方式相互作用的单个波形。
- 这不是您只能立即了解的内容。这需要时间。但是您可能应该花一些时间对此进行认真思考。
- **在任何情况下，人们通常都将记录样本的选择描述为“样本”，并且将样本中的单个幅度值描述为“样本”。两种用法都是正确的**

## Manipulating samples by changing their playback rate, order, and position

- Once you have samples loaded in to memory, you can manipulate them just like any other list of numbers
- For example, you could randomly select samples, or read the samples backwards.
- Two common operations people often want to do are: speeding up the playback rate, and slowing down the playback rate
- You can easily double the speed of playback by only playing back every other amplitude value in the list
- You can also halve the speed of playback by playing every amplitude value twice.
- But how would you play back the sample at 3/4 (75%) speed? To do this you would need to be able to read an array value somewhere between two of the actual array values you have - like this `mySampleArray[1.5];`. This is not possible, as each array index needs to be an integer - an actual index in the list!!
- (you could just use the nearest actual value but this sounds pretty bad)
- A better idea is to work out where you think the amplitude would be at that point in the array if it did exist - e.g. somewhere between two actual values - using **interpolation**.
- 一旦你将样本加载到内存中，你就可以像其他数字列表一样操作它们。
- 例如，你可以随机选择样本，或者倒读样本。
- 人们经常要做的两种操作是：加快播放速度，放慢播放速度。
- 您可以轻松地将播放速度提高一倍，只需播放列表中的每一个其他振幅值。
- 你也可以通过将每个振幅值播放两次，将播放速度减半。
- 但是你如何以3/4（75%）的速度回放样本呢？要做到这一点，你需要能够在你所拥有的两个实际数组值之间的某个地方读取一个数组值--就像这样`mySampleArray[1.5];`。这是不可能的，因为每个数组的索引需要是一个整数--列表中的实际索引!
- (你可以只使用最接近的实际值，但这听起来很糟糕)
- 一个更好的想法是，利用**插值**，计算出您认为振幅在数组中的那个点会在哪里，如果它真的存在的话--例如在两个实际值之间的某个地方。

## Interpolation

- Interpolation means 'estimating a new data point based on known data'
- The most common type of interpolation is called *Linear Interpolation*
- This attempts to plot a straight line between two points, and identify how far along that line you need to be.
- So for example, if array value 1 (point a) has a value of 0.5, and array value 2 (point b) has a value of 1.0, and you are trying to find a value halfway between these (let's call this the remainder, and it's halfway so we can say this is 0.5), you could use the below algorithm:
- `a + ((b - a) * remainder))`
- Basically, take a, and add on half the difference between b and a.

[![Linear Interpolation Graph from Wikipedia Commons](https://camo.githubusercontent.com/9e2adde1df3976364530b7bb98376c1179582978774eb1e841f8c364e459d9d4/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f362f36382f4c696e6561725f696e746572706f6c6174696f6e2e706e67)](https://camo.githubusercontent.com/9e2adde1df3976364530b7bb98376c1179582978774eb1e841f8c364e459d9d4/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f362f36382f4c696e6561725f696e746572706f6c6174696f6e2e706e67) This graph might help you to visualise this process a bit more - although this is a 2D plot, and at the moment we're only really thinking about a 1d signal - but the extra dimension can make it easier to think about. We'll be returning to this idea a few times in the course. In the graph, the new point is (x,y). (x0,y0) and (x1,y1) are what we're calling a and b respectively above.

- Linear interpolation is relatively cheap in terms of computation, and works well for most things, but in audio it can generate noise in the high frequency signal components, as it is literally drawing a straight line between two points where there should instead be a curve.
- Also, in real situations, you need to calculate the remainder on the fly - it won't simply be halfway, and will depend on the playback speed.
- You can do this by subtracting the desired position (where you want to read a value from given your playback speed, e.g. [1.5]) from the nearest prior position (which would be 1 in this case).
- Like this : `remainder = position - Math.floor(position);`
- You can then calculate the imaginary amplitude value at that imaginary position as follows:
- `amplitude = ((1-remainder) * a + remainder * b);`, which is more or less the same as the above.
- An even better interpolation algorithm is cubic interpolation, which augments the above by calculating a curve between the two points with the help of two more points which define the slope. So you get the sample before the closest point (a), the closest point (b), and two of the upcoming points (c and d), and process these using some constants (the values of the constants depend on various factors, and it is actually a matter of taste)
- As an extra bit of information for those that are interested, there are many different cubic interpolation algorithms, and they don't all sound the same, despite the mathematical differences being not very large - this is just the nature of audio, as the ear can be very sensitive. This is one of the **best sounding** cubic interpolation algorithms you will find in my opinion, but :

```
a1 = 0.5 * (c - a); a2 = a - 2.5 * b + 2.0 * c - 0.5 * d; a3 = 0.5 * (d - a) + 1.5 * (b - c); output = (((a3 * remainder + a2) * remainder + a1) * remainder + b);
```

## How to Load a Sample

- You can use the maxiSample object from the Maximilian library
- First you need to create a maxiSample Object: `var mySample = new maximJs.maxiSample();`
- Then you need to load in a sample (make sure you've uploaded an audio file to the MIMIC Platform first - it can be in any format your browser supports)
- Annoyingly, we have to pass the name of the audio file to the sample object you created using the main maxiAudio object (gah!).
- Don't blame me for this. It's a 'design feature' of the webAudio API that we've not been able to work around. `maxiAudio.loadSample('uploaded-sample.wav', mySample);`
- Now you can ask the maxiSample object to pass amplitude values stored in the audio file to the output, or do pretty much anything else you like with it.
- You can also use the maxiSample.play() functions to manipulate the sound by speeding it up, slowing it down, reversing it, triggering based on conditions etc. These mostly use linear interpolation but you can try the play4 method if you wish to listen to the cubic interpolation. Further documentation is available via Chris Kiefer's MIMIC article here (check the section on maxiSample): https://mimicproject.com/guides/maximJS
- You can also control the playback of the sample with any other signal
- Or use the 'playOnce()' function to play the sound only once. You can trigger the sample with the trigger() function This is a fun example that uses cubic interpolation https://mimicproject.com/code/25cecd79-bbce-c8cb-9d78-23501f6933f7
- 使用MIMIC加载和回放样本非常容易
- 您可以使用Maximilian库中的maxiSample对象
- 首先，您需要创建一个maxiSample对象： `var mySample = new maximJs.maxiSample();`
- 然后，您需要加载一个示例（请确保先将音频文件上传到MIMIC平台-该文件可以是您的浏览器支持的任何格式）
- 烦人的是，我们必须将音频文件的名称传递给使用主maxiAudio对象（gah！）创建的样本对象。
- 不要怪我。这是我们无法解决的webAudio API的“设计功能”。 `maxiAudio.loadSample('uploaded-sample.wav', mySample);`
- 现在，您可以要求maxiSample对象将存储在音频文件中的振幅值传递到输出，或者使用它进行几乎任何其他操作。
- 您还可以使用maxiSample.play（）函数通过加速，减速，反转，根据条件触发等方式来操纵声音。这些方法大多使用线性插值法，但是如果您想收听，可以尝试使用play4方法到三次插值。可通过Chris Kiefer的MIMIC文章获得更多文档（请参见maxiSample上的部分）：[https](https://mimicproject.com/guides/maximJS) ://mimicproject.com/guides/maximJS
- 您还可以使用其他任何信号来控制样本的播放
- 或者使用“ playOnce（）”功能只播放一次声音。您可以使用trigger（）函数触发样本。这是一个有趣的示例，使用三次插值 https://mimicproject.com/code/25cecd79-bbce-c8cb-9d78-23501f6933f7

## Introduction to maxiClock

- maxiClock is a simple system for triggering events based on BPM (Beats Per Minute) and 'Ticks' per beat.
- BPM is a means for setting the rate of playback by how many events you want to trigger each minute
- You can also divide up each beat in to more events, called 'ticks'.
- Professional audio systems can have thousands of ticks per beat.
- Most musicians tend to use musical rhythmic concepts, specifically note durations, for dividing up beats.
- A beat is a crotchet, half a beat is a quaver, a quarter of a beat is a semiquaver (four per beat). You can also have demi-semiquavers and hemi-demi-semiquavers.
- Frankly these days you can do what you want.
- The below code sets up a maxiClock object called 'myClock'.
- maxiClock是一个简单的系统，用于根据BPM（每分钟节拍数）和每个节拍“滴答声”触发事件。
- BPM是一种通过每分钟要触发多少事件来设置播放速率的方法
- 您还可以将每个节拍分成更多事件，称为“滴答声”。
- 专业音频系统每个节拍可能有数千个滴答声。
- 大多数音乐家倾向于使用音乐节奏概念（特别是音符持续时间）来划分节拍。
- 拍子是小手，半拍子是八分音，四分之一拍子是四分音（每拍四声）。您也可以使用半脱半数和半脱半数。
- 坦白地说，这些天您可以做自己想做的事。
- 下面的代码设置了一个名为“ myClock”的maxiClock对象。

```
var myClock = new maximJs.maxiClock(); myClock.setTempo(myTempo); myClock.setTicksPerBeat(2);
```

## Triggering a sample with maxiClock

- In order to make the clock count ticks, you need to run the 'maxiClock.ticker()' method in the main maximilian 'play' function.
- So if your maxiClock object is called 'myClock', you need this in 'play': `myClock.ticker();`
- You can then run a test with a conditional to see if there's a clock tick happening, and if there is, make something happen.

```
if( myClock.tick ) { mySample.trigger();}
```

- You can also check to see where the maxiClock playHead is. You can then make things happen if the playHead is before, at or after a certain point:

```
if( myClock.tick && myClock.playHead>=100){ mySample.trigger(); // Also do anything else you fancy }
```

- 为了使时钟计数滴答作响，您需要在主要maximilian“播放”功能中运行“ maxiClock.ticker（）”方法。
- 因此，如果您的maxiClock对象称为“ myClock”，则需要在“ play”中使用： `myClock.ticker();`
- 然后，您可以在有条件的情况下运行测试，以查看是否有时钟滴答发生，如果有，则使某些事情发生。

```
if( myClock.tick ) { mySample.trigger();}
```

- 您也可以查看maxiClock playHead的位置。然后，如果playHead在某个点之前，某个时刻或之后，则可以使事情发生：

```
if( myClock.tick && myClock.playHead>=100){ mySample.trigger(); // Also do anything else you fancy }
```

## Example code for this session:/maxiclock/modulation

- This basic drum machine example has everything you need in it
- https://mimicproject.com/code/9538f995-f184-8a64-967c-f5de93e58076
- Here is a more developed example with the play-button code in it, and a more complex output:
- https://mimicproject.com/code/86a2fefb-4314-16dc-a7d5-fd930bd481d0

# Advanced Example//attern generation, multiple voices// subtractive synthesiser examples.

- Here's an advanced example that combines all the things we looked at in the last two weeks, as well as some other stuff including pattern generation, multiple voices, and fully implemented subtractive synthesiser examples.
- https://mimicproject.com/code/afe3b617-4ad9-97df-6c8c-818b901897eb

# Common Questions

##### 如何根据声音使视觉发生变化？

- How can I make something happen visually based on a sound?

For this you need to do some form of analysis of the sound output. The first method you should probably try is to get the average of a block of samples. This is super easy using the very first example I showed you, as I'm collecting blocks of samples (the sample buffer) which gives us a list 1024 numbers around 40 times a second. You can calculate the mean, and then use this to make something happen. Another method would be to get a spectrogram (using the FFT Analyser - I recommend you check out the excellent tutorial by Nick Collins, which is here on the MIMIC Project website : https://mimicproject.com/guides/mmll ).

- I'm calculating the mean of each sample buffer and this is working OK, but sometimes it seems not to capture the intensity of the signal very well. Is there a better way?

This is because you're smoothing the signal and the peak values are therefore being flattened. You could calculate a better measure by getting the square of each of these 1024 values, getting the mean of all of these squares, and then calculating the square root of that mean. This gives you the **Root Mean Square** output, or **RMS**.

- I tried connecting the mean output of the sound to the parameter of my graphics system, but it's giving me a continuous signal. How can I trigger something based on this instead of just using the value?

You can use a conditional to check if the value goes over a certain amount, and then use this to trigger something. This bit of code is probably a good starting point (you would of course need to define these variables yourself) :

```
if (RMS_Output > 0.5) {myImageTrigger = True;} else {myImageTrigger = False;}
```

- I've got a conditional set up that is setting a boolean value to True whenever the RMS output is over a threshold value (e.g. 0.5). But the problem is, it stays true and then keeps triggering over and over again for the entire length of time that the conditional statement stays true. How can I get it to trigger once, and then not trigger again?

There are about 1000 ways to do this but the easiest method is to have a countdown which locks the conditional in a False state for a short time after it's first been triggered. Something like

```
if (RMS_Output > 0.5 && reTrigCounter < 0) { myImageTrigger = True; reTrigCounter+=someValue;//add some value to the reTrigCounter so it's above zero and won't trigger again next time. } else { myImageTrigger = False; reTrigCounter--//subtract one until you get to zero and you can trigger again }
```

But TBH this is not the best method. It's just the easiest to do if you've not done it before. A better method is to get the mean output of the last n spectral flux values and build an adaptive threshold using standard deviation, for which you'd need to do an FFT as above.

- How can I control the sound with my body?

You could use one of Louis' great tutorials to learn how to do this with your webcam. https://mimicproject.com/code/90def343-a896-31d4-d818-20d89b9bc631

- How can I make more music using machine learning approaches?

More great examples on how to do this !

https://mimicproject.com/guides/learner



# Session 3: 2D Graphics Part One: Graphs, Shapes and Coordinates

[![Still taken from Will Gallia's 'Adventures in Sine](https://camo.githubusercontent.com/1a7bd6f5cc4d70105385d646b670ce2c071d15fbdd94be82e566946f0b8c2739/687474703a2f2f7777772e7767616c6c69612e636f6d2f636f6e74656e742f696d616765732f6169732f73696e65312e6a7067)](https://camo.githubusercontent.com/1a7bd6f5cc4d70105385d646b670ce2c071d15fbdd94be82e566946f0b8c2739/687474703a2f2f7777772e7767616c6c69612e636f6d2f636f6e74656e742f696d616765732f6169732f73696e65312e6a7067)

Still Taken from Will Gallia's "Adventures In Sine", http://www.wgallia.com/content/images/ais/

### Part 2: Visualising Sound waves

#### Let's take another look at the visualisation code we've been using://drawing wave

https://mimicproject.com/code/9e2e7a7f-e1b9-8606-a48b-f50428596cb8

- We can visualise wave forms very easily with maximilian
- We do this by grabbing the audio buffer and writing it to an array
- We can then create a draw loop and use the buffer output to draw lines of different lengths for each amplitude value
- Each time the buffer changes, we get a new frame of audio values
- The different line lengths correspond to the amplitude of the signal described by each value in the buffer.

## Analysing the draw code

- So we know we're going to take each value in the list and use it to create a line
- And the length of the line is based on the size of the value in the audio buffer
- So each frame is a visualisation of each audio buffer
- The reason it appears stationary (isn't moving around) is that we have locked the audio waveform duration to the number of values in each buffer
- We are then dividing up the width of the screen by the number of values in each audio buffer
- This is the default value - 1024.

```
var spacing = (width / 1024);
```

- Then we equally space each line across the screen using a for loop

```
           for (var i = 0; i < 1024; i++) {
                context.beginPath();
                context.moveTo(i * spacing, height / 2);
                context.lineTo(i * spacing, height / 2 + (drawOutput[i] * height / 4));
                context.stroke();
                context.closePath();
            }
```

## Coordinates

- Here, we've been using a rectangular (or cartesian) coordinate system
- This is the system we usually use for drawing when we start out
- https://en.wikipedia.org/wiki/Cartesian_coordinate_system
- Today, we are going to be drawing lots of curves. To do this, we need to use a very different 2D representation called a **Polar Coordinate System**

# John Whitney Senior

- John Whitney Senior is a key figure in computer graphics
- He was originally a composer who used a number of techniques to create experimental music and video art
- Some of his earliest computer graphics work was completed on discarded M5 and M7 targetting computers
- This led to him creating the first computer generated title sequence in 1957

https://www.youtube.com/watch?v=4CZfSc6nJ8U

- Here's an interesting online article on the topic with some photographs of the device he used: https://www.diyphotography.net/alfred-hitchcocks-vertigo-possibly-first-movie-use-computer-animation/
- He and his brother James won a prize at the world's first experimental film festival for a series of works they created in 1944 entitled *Five Abstract Film Exercises*.
- This link is film number 4 from that series. The images are created with pantographs, and the audio is additive synthesis plotted on graph paper, and drawn on to the soundtrack using modified pendulums.

https://www.youtube.com/watch?v=nTEABxz1e_k

In 1961, John Whitney produced this film, which is a Catalogue of artworks comprising some of the world's first computer animation. https://www.youtube.com/watch?v=TbV7loKp69s

This is a fascinating film where John Whitney explains his early computer graphics experiments at IBM https://www.youtube.com/watch?v=jIv-EcX9tUs

https://mimicproject.com/code/a1996d3f-ecf1-75ae-5486-30904042bfcc

### Part 3

#### Using Polar Coordinates//极坐标

- Usually when we draw circles, we call a function to do so

- e.g. we can use the canvas `arc` function, or the p5 `circle` or `ellipse` functions

- When you call the ellipse function in processing, or use the arc function on the JS Canvas the computer runs a function

- That function takes a position value for the centre of the circle (the origin), and a radius (distance from the origin)

- It uses these two values to draw the circle using trigonometry.

- We can do this ourselves using polar to cartesian conversion

  ### 

##### //polar to cartesian conversion//极坐标到笛卡尔的转换的例子

- https://mimicproject.com/code/44f2f678-dfb3-781b-dfa6-860aa56fceb5

## Polar to Cartesian Conversion (POLTOCAR)

- We do this as follows:
- `x = (r * cos( θ ))`
- `y = (r * sin( θ ))`
- θ is the angle in radians (we often call this 'theta', or 'phase')
- r is the radius (or magnitude, or amplitude)
- sin and cos are the mathematical functions we use to create curves
- Together they allow us to work out where x and y are when we are thinking about angles and distances.
- It's almost ALWAYS a good idea to think about angles and distances, and we'll be returning to this idea all the time
- When the radius is equal to 1, we think of the circumference of the circle is `TWO * PI` (`2PI` or `TWOPI` or `2 * 3.14159` or just `6.28318`).
- This means if we know how many segments we want to use to divide up the circle, we can divide TWOPI

## Radius

- The radius / magnitude is the distance from the origin (the centre)
- We can use this to scale coordinates easily
- This is because the angle contains the direction of travel
- When we multiply the angle by the radius, the point we are drawing moves further away from the centre
- It does this in the direction described by the angle
- When we convert from polar coordinates back to cartesian coordinates, the angle is contained in both the x and y coordinate.
- This is why when we multiply both x and y coordinate of a point, it increases in magnitude, and this magnitude is equal to the radius.

## Getting the Radius back - CARTOPOL

- We can use **Pythagoras’ theorem** to convert cartesian coordinates to a radius
- This is because the radius (magnitude) is the length of the hypotenuse from the origin to (x,y)
- This is also incredibly useful for finding out how far away you are from something
- I'm sure you remember this from High School:

[![pythagoras theorem (creative commons license)](https://camo.githubusercontent.com/36edcca58b3ef762bb187417b5fc10b2cc0786c1bc0e4c50044608f3fbd4790d/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f392f39652f5079746861676f7261732d70726f6f662d616e696d2e737667)](https://camo.githubusercontent.com/36edcca58b3ef762bb187417b5fc10b2cc0786c1bc0e4c50044608f3fbd4790d/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f392f39652f5079746861676f7261732d70726f6f662d616e696d2e737667)

## CARTOPOL Theta

- Getting the angle is more complicated - but very useful, as it represents the direction from the origin
- tan( θ ) = y / x So
- θ = tan-1 ( y / x )
- tan-1 is atan() - the inverse tangent
- So the angle in radians = atan(y/x) for positive nonzero numbers
- atan2 is used for all four quadrants of a cartesian coordinate space and cases where x=0
- This is a bit tricky but we will come back to it all the time.

## Circles

- Let’s return to our circle code
- spacing is the distance around the circle
- x = cos(spacing*n)*a
- y = sin(spacing*n)*b

## Drawing Polar Graphs of Waveforms

- We can use this approach to draw the audio waveforms around a circle instead of in a line across the screen
- We do this in the same way, but instead of joining up points around the circle, we draw lines of different lengths
- The lines are spaced around the circle
- They are drawn from the centre of the circle (amplitude = 0) to the edge (maximum amplitude)
- When we do this, we can see the phase wrapped around the c
- The length of the lines is the amplitude of the value in the array
- https://mimicproject.com/code/a7e2f833-49c8-d71f-99bd-19a993321e7e

## Synthesising 2D Waveform Graphs Directly

- Let's build a simple system for creating polar curves without audio
- This is a simple form of one of John Whitney's favorite algorithms, which he referred to as *The Roses of Grandii*
- The original curve was created by Luiugi Guido Grandii in 1728. It's called *Flores geometrici* and is very well known
- You can find plenty of examples of Flores geometrici on the web in fairly complex form.
- There's quite a boring article on the algorithm on Mathematica. https://mathworld.wolfram.com/Rose.html
- The version we are going to create is the basic curve as described above.
- Here's most of the code...

```
  let canvas = document.querySelector("canvas");
  let context = canvas.getContext("2d");
  canvas.width = 800;
  canvas.height = 600;
  
  var radius = 100;
  var penSize = 5;
  var positionX = 200
  
  var draw = function() {

    for (var i = 0; i<500; i++) {

    context.fillRect(positionX+Math.cos(i*Math.sin(i))*radius,positionX+ Math.sin(i *Math.sin(i))*radius,penSize,penSize);
    }
    requestAnimationFrame(draw);
    
  }
  
  requestAnimationFrame(draw);
```

# Session 3 Homework

- Here's a slightly more developed version of *Flores geometrici* that uses the mouse to control the formation of the petals

##### mouse控制，极坐标与笛卡尔坐标转换的例子// *Flores geometrici

- https://mimicproject.com/code/a1996d3f-ecf1-75ae-5486-30904042bfcc
- 介绍了圆周围的间距，创建谐波，音频可视化
- Notice that this one calculates the spacing around the circle and uses this as a parameter to create harmonics, similar to those we saw in the audio visualisation

summary

- basic 2D graphics concepts基本的2D图形概念
- We looked at simple canvas drawing functions and how we can use them to graph functions
- We learned about cartesian and polar coordinate systems
- We also looked at how to convert between polar and cartesian coordinates (super important)如何在极坐标和笛卡尔坐标之间转换
- We learned how to draw circles from scratch using trigonometry, and how this can be used as a basis for understanding how to create different kinds of curves
- We learned about how the radius of a circle can describe the magnitude of something and also the distance between things
- We also thought a little about how this is the same as calculating the hypoteneuse of a right-angled triangle, and is also the l2Norm / Euclidean Distance
- We looked at how the position around a circle is an angle in radians, which we can call Theta, or Phase, depending on what we're thinking about
- We then looked at how we can use this knowledge to visualise periodic signals in polar space
- We learned about how early computer graphics pioneers such as John Whitney used these approaches to create the first 2D and 3D computer graphics systems, and how these stylistically related to early abstract cinema and classical geometry.
- I then set you all a task to take a more complex variant of this form called *Flores Geometrici*, and use it as a starting point to create your own interactive (or *reactive*) 2D asbtract artwork.

- 我们了解了圆的半径如何描述事物的大小以及事物之间的距离
- 我们还仔细考虑了这与计算直角三角形的斜边的相同之处，也是l2Norm /欧几里德距离
- 我们研究了圆周围的位置如何以弧度表示一个角度，我们可以将其称为Theta或Phase，这取决于我们在考虑什么
- 然后，我们研究了如何使用这些知识来可视化极地空间中的周期性信号
- 我们了解了诸如John Whitney之类的早期计算机图形学先驱如何使用这些方法创建了第一个2D和3D计算机图形系统，以及它们在样式上与早期的抽象电影和古典几何之间的关系。
- 然后，我将所有任务都设置为采用这种称为*Flores Geometrici的*形式的更复杂的变体，并将其用作创建自己的交互式（或*反应性*）2D抽象艺术品的起点。

# Session 4: Pixel Manipulation and Image Processing

[![Mandala Image from Wikimedia commons](https://camo.githubusercontent.com/a0a6e526b3a33020c7bf0f86abbfd336d39cdc46b7a3850757c3627727910b36/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f392f39612f4d616e64616c615f35322e737667)](https://camo.githubusercontent.com/a0a6e526b3a33020c7bf0f86abbfd336d39cdc46b7a3850757c3627727910b36/68747470733a2f2f75706c6f61642e77696b696d656469612e6f72672f77696b6970656469612f636f6d6d6f6e732f392f39612f4d616e64616c615f35322e737667)



### Part Two : Using Expressions to Fill Space

#### Creating Images From Scratch

- The algorithms we used for creating the polar line drawings are basic geometric 'expressions'
- 像素点绘图 draw filled shapes using similar expressions
- https://mimicproject.com/code/f3a32c49-7c24-556f-af1b-91315be36ad9
- The above example uses the 'createImageData()' method to draw some concentric rings.
- We iterate through every pixels on the canvas
- We then decide what colour each pixel should be by using a simple expression

##### Writing output pixels//设置rgb通道

- set red, green, blue, and alpha:

```
position=(x+y*imageData.width)*4;
imageData.data[position] = c%255;
imageData.data[position+1] = c%255;
imageData.data[position+2] = c%255
imageData.data[position+3] = 255;
```

- The modulo operator is to ensure that the output never goes over 255,

- The 'position' line moves through the Image Data 'array', writing colour channels for each position.

- position "行在Image Data "数组 "中移动，为每个位置写入颜色通道。

  

## Another simple expression/rgb通过&三角函数创造像素图案

- https://mimicproject.com/code/bfcbcefb-ba11-f96b-21f5-7a6629ee7e61
- This algorithm uses trigonometric functions across both X and Y



#### Part Three : Lecture

#### Review: Pixel Formats

- In JavaScript, pixels are held in imageData buffers像素被保存在imageData缓冲区

- As we've seen we can write values directly in to imageData buffer arrays

  如何访问像素dimensional arrays：nested for loops to help us access and create data as columns and rows

- each pixel position (i,j) actually has **4** values in the array that it needs in order to create the pixel

- These four values are the **RED, GREEN, BLUE and ALPHA** channel colour values

- 每个像素位置（i，j）实际上在数组中具有创建像素所需的**4个**值

- 这四个值是**红色，绿色，蓝色和ALPHA**通道颜色值

- Each value is an 8-bit value, meaning that each pixel is represented by 32 bits of information (8 bits per channel).

- This means that when we are trying to process imageData arrays, to get to pixel (50,10) of a 100 * 100 image, we actually need to get to array value **((50 \* 100) +10) 4**. At that point, we will then find 4 values - the actual RGBA data for that pixel.

- As a formula, where w is the imageWidth, j is the x coordinate, and i is the y coordinate, this is `((y*imageWidth)+x)*colourChannels`

- 作为一个公式，其中w是图像宽度，j是x坐标，i是y坐标，这就是((y**图像宽度)+x)*colourChannels。

- So the code you would need to access this pixel in JavaScript is actually: `imageData.data[((50 * 100)+10) * 4];`

  

- We use nested for loops to make accessing the pixel data easier. We can treat `i` as the column variable (the `y` axis value). We can then cycle through all the row values, usually referred to as `j` (the `x` axis values) at that column position.

- We do this by multiplying `i` by the image width (which gives us one whole row for each `i`), then adding the current row pixel value j (the `x` value).

- Finally, to account for the fact that the actual size of the array is 4 times the image dimensions, we multiply by 4. This will land us on the RED pixel value for that `(i,j)` coordinate - like this: `imageData.data[((imageWidth * i) + j) * 4] = 255; // set the RED pixel at i to its maximum value of 255`

- Finally, to access the Blue colour value you would need to do this: `imageData.data[((imageWidth * i) + j) * 4 + 2] = 255; // set the Blue pixel at i to its maximum value of 255`

- This is because the position in the pixel array + 1 is Green, +2 is Blue, and +3 is Alpha.

- 每个值都是一个8位的值，也就是说每个像素由32位的信息代表（每个通道8位）。

  这意味着，当我们试图处理imageData数组时，要得到100*100图像的像素（50,10），我们实际上需要得到数组值（（50*100）+10）4。这时，我们就会找到4个值--该像素的实际RGBA数据。

  作为一个公式，其中w是图像宽度，j是x坐标，i是y坐标，这就是((y*图像宽度)+x)*colourChannels。

  因此，你需要在JavaScript中访问这个像素的代码实际上是：imageData.data[((50 * 100)+10) * 4]。

  记住，在许多平台/不同的语言中，像素数据并不是RGBA格式的。不过在JavaScript中，它大多数情况下都是这样的，但这实际上是你的工作，所以要确保你知道。这真的很重要。

  我们使用嵌套for循环来使访问像素数据更容易。我们可以将i视为列变量（y轴的值）。然后我们可以循环浏览该列位置的所有行值，通常称为j（x轴值）。

  我们通过将i乘以图像宽度（这使我们对每i都有一整行），然后加上当前行像素值j（x值）来实现。

  最后，为了考虑到数组的实际大小是图像尺寸的4倍，我们乘以4。 这将使我们得到该(i,j)坐标的RED像素值--就像这样：imageData.data[((imageWidth * i) + j) * 4] = 255; // 将i处的RED像素设置为最大值255。

  最后，要访问蓝色的颜色值，你需要这样做：imageData.data[((imageWidth * i) + j) * 4 + 2] = 255; //将i处的蓝色像素设置为最大值255。

  这是因为像素数组中的位置+1是绿色，+2是蓝色，+3是Alpha。

## Basic Image Processing

- load an image and perform basic operations in order to alter it： use 'getImageData()' to do this

- In the below example, we use the > operator to threshold the image

- threshold. example：

- https://mimicproject.com/code/6f02256b-bd70-e782-054b-435ad3ac8eaa

- You might need to press 'play' to get the image to load.

- This example is a threshold.

- What else could we do?

- Could we invert the threshold? What would this do?

-  increase the brightness/example：

-  https://mimicproject.com/code/88d46039-0070-4826-6692-ca70d8ac90f8

- How could we increase the contrast? Here's one way? : https://mimicproject.com/code/85301f88-5d44-8dc3-f4c5-0d329c452122

- Well yes of course. For example, we can generate brightness by interpolating the current pixel value against 0. We could generate contrast by interpolating the current pixel value against gray (which is sort of what we did). Finally, we could create saturation by interpolating the current pixel value against it's own luminance. You can generate luminance very easily with the following formula: `(0.2126*R + 0.7152*G + 0.0722*B)`.

- Once you have this value for the pixel, you could interpolate a new value by doing something like this: `(1 – saturation_value) * pixel_luminance + saturation_value * actual_pixel_value`

- This is v. similar to what we did when we interpolated new values for changing the speed of audio sample playback.

- 我们可以通过将当前像素值与0进行内插来产生亮度，我们也可以通过将当前像素值与灰色进行内插来产生对比度（这就是我们所做的），最后，我们可以通过将当前像素值与自身亮度进行内插来产生饱和度。最后，我们可以通过将当前像素值与它自身的亮度进行内插来生成饱和度。你可以用下面的公式非常容易地生成亮度。(0.2126*R + 0.7152*G + 0.0722*B).

  一旦你有了这个像素的值，你可以通过这样的方法插值一个新的值。(1 - 饱和度值) * pixel_luminance + 饱和度值 * actual_像素值

  这与我们在插值改变音频样本播放速度时所做的事情很相似。

## Rotating an Image by Hand

- In most Creative Coding frameworks you can just call 'rotate' to rotate an image.
- But it's worthwhile taking a look at how this actually works
- The below example shows how we can use something similar to the circle formula from last week to rotate each pixel to a new location on the screen.
- 旋转图像
- https://mimicproject.com/code/86c8ecc8-4fb7-a25b-448d-a05e3fb4b6ed
- There are two important parts to this code. First we need to calculate which pixel we want to move, and use a 2D rotation to move it.

```
// This is a 2D matrix rotation!!! It's very similar to the code we used to rotate points around a circle.
var x = Math.floor((Math.cos(theta) * j) - (Math.sin(theta) * i));
var y = Math.floor((Math.sin(theta) * j) + (Math.cos(theta) * i));
```

- j is the current pixel's original Y position, i is the current pixel's original X position.
- j and i here are acting like the radius of the circle
- theta is the angle, or how far round the circle we want to rotate
- We use Math.floor to round down, as this is an actual pixel xy coordinate. If we don't do this, things could get messy
- The two new vars, x and y, are going to be where we are copying from - we want these colour values to be written to the current pixel
- The next bit of code does that part:

```
imageData2.data[((imageWidth * i) + j) * 4] = data[((imageWidth * y) + x) * 4];
```

- We are using the rotation code to work out which pixel we actual want to write in to the imageData buffer at that point. This means we need to calculate a rotation for every i j, and write the pixel values - all four of them (RGBA) from where they are, back to where we want them!

## Additional Materials: Rotation Code with Zooming, Offsets and Anchors

- 改变旋转原点
- People often aske how to change the origin of a rotation.
- To do this, you need to make adjustments to the Matrix rotation.
- We are adding parameters to translate the origin, translate the image, and scale (zoom) the image.
- Below is the code with the important changes:

```
// Rotation, translate (offset), origin translate (anchor) and scale (zoom)

var x = Math.floor((Math.cos(theta)/zoomX) * (j-(offsetX+anchorX)) - (Math.sin(theta)/zoomY) * (i-(offsetY+anchorY)))+anchorX;
var y = Math.floor((Math.sin(theta)/zoomX) * (j-(offsetX+anchorX)) + (Math.cos(theta)/zoomY) * (i-(offsetY+anchorY)))+anchorY;
```

- Here's a link to a document with the above included:
- https://mimicproject.com/code/e9d8b9db-7e79-8aaa-9ec2-e672cd76eaa9

## Image Processing using Convolution

- We can produce a wide range of image processing effects with a process called 'convolution'
- Convolution allows us to perform blurs, edge detections and other common filter processes
- To do this, we create what is called a 'kernel', which is a small grid of numbers, 3 * 3 for example.
- The kernel decides what the central output pixel should be by multiplying the surrounding pixels by values in the grid
- After the multiplications, all the values get added together and averaged to find the value for the centre pixel.
- The below is an excellent visual explanation of image kernels.
- http://setosa.io/ev/image-kernels/
- There are even more here:
- http://aishack.in/tutorials/image-convolution-examples/

## Performing an Edge Detection / Gradient analysis

- Here's an example that uses the simplest possible approach to perform an edge detection
- This edge detection is very efficient and actually very powerful
- https://mimicproject.com/code/e9e74da1-ecd7-719d-9c8c-51d5b52d4cad
- (remember to press the play button if the images don't appear)
- The example uses a very very simple image processing approach which is operating in place, rather than as a separate array
- So we're taking a short-cut (no convolution kernel, just manual multiplication of pixels)
- It uses a 'kernel' of -1 0 1 in **only one dimension**. You can select either the X or Y dimension to see the effect.
- This produces a basic edge detection - but it can do much much more than this.

```
imageData2.data[((imageWidth * i) + j) * 4] = (-1*(data[((imageWidth * i) + j-1) * 4])) + (data[((imageWidth * i) + j+1) * 4]);
```

- The above code takes the pixel before the current position, and multiplies it by -1, which inverts it (so 128 would become -128).

- It then takes the pixel **after** the current pixel (e.g. 128) and adds it (it ignores the data in the current pixel entirely).

- This gives you a new image which only contains **the difference between the previous pixel and the next pixel**

- 上面的代码取当前位置之前的像素，并将其乘以-1，使其反转（所以128会变成-128）。

  然后取当前像素之后的像素(例如128)并将其相加(它完全忽略了当前像素中的数据)。

  这样就得到了一个新的图像，它只包含上一个像素和下一个像素之间的差值。

- In the above example, the output pixel value would be 0. This would mean that **nothing in the image had changed at that point**

- This produces what we call `gradients`

- These can be used to create edge detection, but frankly, the gradients are much more powerful than that.

## Gradients的作用！

- The gradients are either across X or Y, and are the basis of simple computer vision approaches
- They tell you where the most change occurs in the image, with pixels representing where the greatest differences are between parts of the image
- If you get two image buffers, one with the X gradients, and one with the Y gradients, you can then do some cool things
- For example, you can run through all the gradients performing a cartesian to polar conversion on the average of groups of pixel gradients
- This can tell you what the magnitude and direction of the gradients are at those points.
- You can use this information to spot things in images, for example, the characteristic curves of the human body and face.

梯度跨越X或Y，是简单的计算机视觉方法的基础。

它们告诉你图像中变化最大的地方，像素代表图像各部分之间差异最大的地方。

如果你得到两个图像缓冲区，一个是X渐变，一个是Y渐变，你就可以做一些很酷的事情。

例如，你可以运行所有的梯度，在像素梯度组的平均值上执行卡提斯到极值的转换。

这可以告诉你这些点的梯度的大小和方向是什么。

你可以利用这些信息来发现图像中的东西，例如，人体和面部的特征曲线。



##### mandelbrot set

- https://mimicproject.com/code/95b09168-00c1-b781-1cf1-9ba3761c276d

##  