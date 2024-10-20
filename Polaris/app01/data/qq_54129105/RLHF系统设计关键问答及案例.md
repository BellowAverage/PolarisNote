
--- 
title:  RLHF系统设计关键问答及案例 
tags: []
categories: [] 

---


#### 目录
- - <ul><li>- - - - - - - 


## RLHF介绍

RLHF（Reinforcement Learning with Human Feedback，人类反馈强化学习）虽是热门概念，但并非包治百病的万用仙丹。本问答探讨RLHF的适用范围、优缺点和可能遇到的问题，供RLHF系统设计者参考。

### RLHF是什么

强化学习利用奖励信号训练智能体。有些任务并没有自带能给出奖励信号的环境，也没有现成的生成奖励信号的方法。为此，可以搭建奖励模型来提供奖励信号。在搭建奖励模型时，可以用数据驱动的机器学习方法来训练奖励模型，并且由人类提供数据。我们把这样的利用人类提供的反馈数据来训练奖励模型以用于强化学习的系统称为人类反馈强化学习，示意图如下。

<img src="https://img-blog.csdnimg.cn/4b08db29963c4107aff220cb1d22ce25.png" alt="在这里插入图片描述"> 图： 人类反馈强化学习：用人类反馈的数据训练奖励模型，用奖励模型生成奖励信号

### RLHF适用于哪些任务

RLHF适合于同时满足下面所有条件的任务： 要解决的任务是一个强化学习任务，但是没有现成的奖励信号并且奖励信号的确定方式事先不知道。为了训练强化学习智能体，考虑构建奖励模型来得到奖励信号。 反例：比如电动游戏有游戏得分，那样的游戏程序能够给奖励信号，那我们直接用游戏程序反馈即可，不需要人类反馈。 反例：某些系统奖励信号的确定方式是已知的，比如交易系统的奖励信号可以由赚到的钱完全确定。这时直接可以用已知的数学表达式确定奖励信号，不需要人工反馈。

不采用人类反馈的数据难以构建合适的奖励模型，而且人类的反馈可以帮助得到合适的奖励模型，并且人类来提供反馈可以在合理的代价（包括成本代价、时间代价等）内得到。如果用人类反馈得到数据与其他方法采集得到数据相比不具有优势，那么就没有必要让人类来反馈。

### RLHF和其他构建奖励模型的方法相比有何优劣

奖励模型可以人工指定，也可以通过有监督模型、逆强化学习等机器学习方法来学习。RLHF使用机器学习方法学习奖励模型，并且在学习过程中采用人类给出的反馈。 比较人工指定奖励模型与采用机器学习方法学习奖励模型的优劣： 这与对一般的机器学习优劣的讨论相同。机器学习方法的优点包括不需要太多领域知识、能够处理非常复杂的问题、能够处理快速大量的高维数据、能够随着数据增大提升精度等等。机器学习算法的缺陷包括其训练和使用需要数据时间空间电力等资源、模型和输出的解释型可能不好、模型可能有缺陷、覆盖范围不够或是被攻击（比如大模型里的提示词注入）。 比较采用人工反馈数据和采用非人工反馈数据的优劣： 人工反馈往往更费时费力，并且不同人在不同时候的表现可能不一致，并且人还会有意无意地犯错，或是人类反馈的结果还不如用其他方法生成数据来的有效，等等。我们在后文会详细探讨人工反馈的局限性。采用机器收集数据等非人工反馈数据则对收集的数据类型有局限性。有些数据只能靠人类收集，或是用机器难以收集。这样的数据包括是主观的、人文的数据（比如判断艺术作品的艺术性），或是某些机器还做不了的事情（比如玩一个AI暂时还不如人类的游戏）。

### 什么样的人类反馈才是好的反馈

好的反馈需要够用。 反馈数据可以用来学成奖励模型，并且数据足够正确、量足够大、覆盖足够全面，使得奖励模型足够好，进而在后续的强化学习中得到令人满意的智能体。 部分涉及的评价指标包括：对数据本身的评价指标（正确性、数据量、覆盖率、一致性），对奖励模型及其训练过程的评价指标、对强化学习训练过程和训练得到的智能体的评价指标。 好的反馈需要是可得的反馈。 反馈需要可以在合理的时间花费和金钱花费的情况下得到，并且在成本可控的同时不会引发其他风险（如法律上的风险）。 部分涉及涉及的评价指标包括：数据准备时间、数据准备涉及的人员数量、数据准备成本、是否引发其他风险的判断。

### RLHF算法有哪些类别，各有什么优缺点

RLHF算法有以下两大类：用监督学习的思路训练奖励模型的RLHF、用逆强化学习的思路训练奖励模型的RLHF。 1.在用监督学习的思路训练奖励模型的RLHF系统中，人类的反馈是奖励信号或是奖励信号的衍生量（如奖励信号的排序）。 接反馈奖励信号和反馈奖励信号衍生量各有优缺点。这个优点在于获得奖励参考值后可以直接把它用作有监督学习的标签。缺点在于不同人在不同时候给出的奖励信号可能不一致，甚至矛盾。反馈奖励信号的衍生量，比如奖励模型输入的比较或排序。有些任务给出评价一致的奖励值有困难，但是比较大小容易得多。但是没有密集程度的信息。在大量类似情况导致某部分奖励对应的样本过于密集的情况下，甚至可能不收敛。 一般认为，采用比较类型的反馈可以得到更好的性能中位数，但是并不能得到更好的性能平均值。 2.在用逆强化学习的思路训练奖励模型的RLHF系统中，人类的反馈并不是奖励信号，而是使得奖励更大的奖励模型输入。即人类给出了较为正确的数量、文本、分类、物理动作等，告诉奖励模型在这时候奖励应该比较大。这其实就是逆强化学习的思想。 这种方法与用监督学习训练奖励模型的RLHF相比，其优点在于，训练奖励模型的样本点不再拘泥于系统给出的需要评判的样本。因为系统给出的需要评估奖励的样本可能具有局限性（因为系统没有找到最优的区间）。 在系统搭建初期，还可以将用户提供的参考答案用于把最初的强化学习问题转化成模仿学习问题。 这类设计还可以根据反馈的类型进一步分类，一类是让人类独立给出专家意见，另一类是在让人类在已有数据的基础上进行改进。让人类提供意见就类似于让人类提供模仿学习里的专家策略（当然可能略有不同，毕竟奖励模型的输入不只有动作）。让用户在已有的参考内容上修改可以减少人类每个标注的成本，但是已有的参考内容可能会干扰到人类的独立判断（这个干扰可能是正面的也可能是负面的）。

### RLHF采用人类反馈会带来哪些局限

前面已经提到，人类反馈可能更费时费力，并且不一定能够保证准确性和一致性。除此之外，下面几点会导致奖励模型不完整不正确，导致后续强化学习训练得到的智能体行为不能令人满意。

1.提供人类反馈的人群可能有偏见或局限性。

这个问题和数理统计里的对样本进行抽样方法可能遇到的问题类型。为RLHF系统提供反馈的人群可能并不是最佳的人群。有的时候出于成本、可得性等因素，会选择人力成本低的团队，但是这样的团队可能在专业度不够，或是有着不同的法律、道德和宗教观念，包括歧视性信息。反馈人中可能有恶意者，会提供有误导性的反馈。

2.人的决策可能没有机器决策那么高明。 在一些问题上，机器可以比人做的更好，比如对于象棋围棋等棋盘游戏，真人就比不过人工智能程序。在一些问题上，人能够处理的信息没有数据驱动的程序处理的信息全面。比如对于自动驾驶的应用，人类只能根据二维画面和声音进行决策，而程序能够处理连续时间内三维空间的信息。所以在理论上人类反馈的质量是不如程序的。

3.没有将提供反馈的人的特征引入到系统。 每个人都是独一无二的：每个人有自己的成长环境、宗教信仰、道德观念、学习和工作经历、知识储备等，我们不可能把每个人的所有特征都引入到系统。在这种情况下，如果忽略不同的人之间在某个特征维度上的差别，那么就会损失到许多有效信息，导致奖励模型性能下降。

以大规模语言模型为例，用户可以通过提示工程指定模型以某种特定的角色或沟通方式来沟通，比如有时要求语言模型的输出文字更有礼貌更客套多奉承套，有时需要输出文字内容掷地有声言之有物少客套；有时要求输出文字更有创造性，有时要求输出文字尊重事实更严谨；有时要求输出简洁扼要，有时要求输出详尽完备提供更多细节；有时要求输出中立客观仅在纯自然科学范围内讨论，有时要求输出多考虑人文社会的环境背景。而提供反馈数据的人的不同身份背景和沟通习惯可能正好对应于不同情况下的输出要求。这种情况下，反馈人的特性就非常重要。

4.人性可能导致数据集不完美。

比如语言模型可能会通过拍马屁、戴高帽等行为获得高分评价，但是这样的高分评价可能并没有真正解决问题，有违系统设计的初衷。看似得分很高，但是高得分可能是通过避免争议性话题或是拍马屁拍出来的，而不是真正解决了需要解决问题，没有达到系统设计的初衷。

此外，人类提供反馈还有其他非技术上面的风险，比如泄密等安全性风险、监管法律风险等。

### 如何降低人类反馈带来的负面影响

针对人类反馈费时费力且可能导致奖励模型不完整不正确的问题，可以在收集人类反馈数据的同时就训练奖励模型、训练智能体，并全面评估奖励模型和智能体，以便于尽早发现人类反馈的缺陷。发现缺陷后，及时进行调整。

针对人类反馈中出现的反馈质量问题以及错误反馈，可以对人类反馈进行校验和审计，如引入已知奖励的校验样本来校验人类反馈的质量，或为同一样本多次索取反馈并比较多次反馈的结果等。

针对反馈人的选择不当的问题，可以在有效控制人力成本的基础上，采用科学的方法选定提供反馈的人。可以参考数理统计里的抽样方法，如分层抽样、整群抽样等，使得反馈人群更加合理。

对于反馈数据中未包括反馈人特征导致奖励模型不够好的问题，可以收集反馈人的特征，并将这些特征用于奖励模型的训练。比如，在大规模语言模型的训练中可以记录反馈人的职业背景（如律师、医生等），并在训练奖励模型时加以考虑。当用户要求智能体像律师一样工作时，更应该利用由律师提供的数据学成的那部分奖励模型来提供奖励信号；当用户要求智能体像医生一样工作时，更应该利用由医生提供的数据学成的那部分奖励模型来提供奖励信号。

另外，在整个系统的实施过程中，可以征求专业人士意见，以减小其中法律和安全风险。

### 案例

RLHF教学题目：培养未来AI领袖

RLHF（Reinforcement Learning with Human Feedback）教学是一种创新的人工智能教育方法，旨在培养具备强化学习和人类反馈技能的人才。本文将介绍RLHF教学的原理、代码实现以及在实际教学中的应用。

一、RLHF教学原理

RLHF教学结合了强化学习和人类反馈，通过让AI系统与人类互动，从而学习人类的行为和价值观。这种教学方法使得AI系统能够更好地理解人类意图，提高决策的准确性。

二、代码实现

以下是一个简单的RLHF教学示例代码，使用Python编写：

```
import numpy as np
import gym

# 创建环境
env = gym.make('CartPole-v0')

# 初始化参数
learning_rate = 0.01
gamma = 0.99
epsilon = 1.0
epsilon_decay = 0.995
min_epsilon = 0.01
max_steps = 200
batch_size = 32
memory_size = 1000
num_episodes = 1000

# 定义神经网络模型
class Model(object):
    def __init__(self, input_size, output_size, hidden_size):
        self.input_size = input_size
        self.output_size = output_size
        self.hidden_size = hidden_size
        self.weights1 = np.random.randn(self.input_size, self.hidden_size)
        self.weights2 = np.random.randn(self.hidden_size, self.output_size)

    def predict(self, state):
        hidden = np.dot(state, self.weights1)
        output = np.dot(hidden, self.weights2)
        return output

# 训练过程
def train(model, env, num_episodes):
    memory = []
    for episode in range(num_episodes):
        state = env.reset()
        done = False
        steps = 0
        while not done and steps &lt; max_steps:
            # 选择动作
            if np.random.uniform() &lt; epsilon:
                action = env.action_space.sample()
            else:
                action = np.argmax(model.predict(state))
            # 执行动作，获得反馈
            next_state, reward, done, _ = env.step(action)
            memory.append((state, action, reward, next_state, done))
            state = next_state
            steps += 1
        # 更新模型参数
        batch = np.array(memory[:batch_size])
        states = np.array([t[0] for t in batch])
        actions = np.array([t[1] for t in batch])
        rewards = np.array([t[2] for t in batch])
        next_states = np.array([t[3] for t in batch])
        dones = np.array([t[4] for t in batch])
        targets = rewards + gamma * (1 - dones) * np.max(model.predict(next_states), axis=1)
        predicted = model.predict(states)
        loss = np.mean((targets - predicted[np.arange(batch_size), actions]) ** 2)
        gradients = np.zeros_like(model.weights1)
        for i in range(batch_size):
            gradient1 = np.dot(states[i], model.weights2[actions[i]]) - targets[i]
            gradient2 = np.outer(gradient1, states[i])
            gradients += gradient2
        model.weights1 -= learning_rate * gradients / batch_size
        model.weights2 -= learning_rate * np.dot(states.T, gradient1) / batch_size
    return model

```

以上代码实现了一个简单的RLHF教学示例，通过训练一个神经网络模型来玩CartPole游戏。在这个示例中，模型通过与环境互动，逐步学习如何玩好这个游戏。人类可以通过调整参数和观察模型的表现来提供反馈，从而改进模型的表现。三、实际应用在教学领域，RLHF方法可以帮助学生更好地理解复杂的概念和问题。通过与人类互动，学生可以逐渐学习如何像人类一样思考和解决问题。同时，RLHF方法也可以帮助企业提高自动化决策的准确性和效率。通过训练AI系统学习人类的决策过程，可以减少错误和不必要的损失。总之，RLHF教学是一种创新的人工智能教育方法，可以培养具备强化学习和人类反馈技能的人才。通过结合代码实现和实际应用，我们可以更好地理解和应用RLHF方法，为未来AI领袖的培养做出贡献。
