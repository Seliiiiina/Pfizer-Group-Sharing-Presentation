# 演讲稿

## Page 1｜Opening

大家好，随着 AI 这两年的快速发展，我们使用 AI 的方式其实也在不断变化，从最开始比较简单的问答，到现在越来越多地尝试把 AI 放进真实的工作任务和流程里面。和大家分享一下我们在这个使用过程中探索的一些 steps：我们怎么从最开始和 AI 来回聊天，逐渐走到一个可以重复执行、检查和改进的工作方式，以及在这个过程中怎么节省token

## Page 2｜From Chat to Reliable Work

如果把所有的内容放在一条线上，大概是这样的。一开始，我们有一个问题，就直接去问 AI。但当任务开始变得复杂之后，我们会发现只靠 Chat 往往是不够的。第一步，我们需要给 AI 一个更清楚的 Structured Prompt，让 AI 知道到底要做什么、按照什么规则做，以及最后要交付什么。但 Prompt 写清楚以后，问题还没有结束。随着文件、修改和对话越来越多，我们会遇到第二个问题：AI 现在到底在用哪些信息？哪些要求还是有效的？ 这就进入了 Managed Context。接下来还有第三个问题：即使 AI 用对了信息，它给我的结果到底能不能直接用、能不能验证？所以我们还需要考虑 Verifiable Output。

当 Prompt、Context 和验证方式都逐渐稳定以后，我们就可以把一次成功的做法保存成可重复使用的模版。如果任务需要经常重复，就可以进一步变成 Workflow。而如果下一步不是提前固定好的，而是需要 AI 根据当前结果自己决定接下来做什么，这时候才开始进入 Agent。

所以这条线上其实有三个问题：

- 我们怎么给 AI 更清晰、更有效的指令？
- 在 Context 变得混乱之前，我们应该怎么管理它？
- 我们怎么把有效的 AI 交互，变成可以重复执行的 Workflow，甚至进一步变成 Agent？

今天这一部分主要涉及在前面这段Prompt、Context 和 Output 这部分

## Page 3｜From Chat to Structured Prompt

我们先把这个 case 过一下。这里用的是一组 mock data，假设明天要做 deliverable review，Leader 发来五个文件，希望我们提前 review 一下 AE summary，看看有没有 issues or inconsistencies。

这五个文件各自是干什么的？ADSL 是 subject-level data，我们用它确认哪些 subject 属于 safety population，以及每个 treatment group 的 denominator。ADAE 是 AE data，我们从这里检查每个 subject 的 AE，以及对应的 SOC 和 PT。RTF 是这次要 review 的 table，analysis specification 告诉我们应该按照什么规则统计，program log 则帮助我们检查运行时的 warning。

所以这个任务其实是拿着 source data 和 specification，去核对已经生成的 AE table。比如 population 对不对？counts 和 percentages 能不能对上？排序有没有按照 spec？log 里面的 warning 有没有影响结果？

但我们让 AI 做的时候，很可能只把文件丢进去，然后说一句：“Please review these files and tell me if there are any issues.”大家看这里 AI 的回答，它确实提到了 Placebo issue，也提到了 counts、percentages 和 program log。乍一看，好像该说的都说了。

我们先看绿色部分。它说“appears to have a Placebo issue”，那到底只是怀疑，还是已经能够确认？它又说“some percentages and a few counts”，那具体是哪几行，现在是多少，应该是多少？最后说“review with the programmer”，那 programmer 接下来到底要检查什么，修正以后又要怎么确认？这些还没有讲清楚。

再看黄色部分。我们自己的 request 其实也没有定义清楚：“any issues”要检查到什么程度？“tell me”是要一段总结，还是一个可以逐项处理的 issue list？如果这件事由我们自己来做，很多要求可能已经在脑子里了。但 AI 只看到了这句话，它不知道我们默认的 review standard 是什么。

所以接下来，我们就用同一个 case 看一下，这些 hidden assumptions 怎么写进 prompt。

## Page 4｜From Vague Request to Structured Prompt

这页左边把刚才省略的东西拆成了五部分：Context、Task、Input、Rules 和 Output。我们先沿着这个 case 看一遍，再看右边完整的 prompt。

Context 是为什么要做。这里就是为了明天的 deliverable review。Task 是具体做什么：核对 AE summary，找出能够确认的问题和不一致。Input 则要把刚才那五个文件的角色说清楚，不能默认 AI 知道哪个是 source，哪个是 output，哪个决定统计规则。

中间这句话想表达的就是，我们平时默认的一些工作规则，需要主动告诉 AI。比如下面这句“Check whether the AE summary is correct.”看起来很明确，但 correct 到底怎么判断？这就要落到 Rules 上。

我们先过一下 denominator。按照这个 case 的 spec，safety population 要用 SAFFL=Y。ADSL 里面 Placebo 一共有六个 subject，但 SUBJ012 的 SAFFL=N，所以 safety denominator 应该是五，而 RTF 表头写的是六。这里我们就可以给出一个具体 finding：Placebo N=6，应该改成 N=5，依据是 ADSL 和 specification。

再看 Any AE。我们要数的是发生 AE 的 subject，不是 ADAE 的记录条数。同一个 subject 有多条 AE，在 Any AE 这一层也只能算一次；在每个 SOC、每个 PT 里面，同样要分别去重。按这个规则，Placebo safety population 里面有四个人发生过 AE，所以应该是 4/5，也就是 80.0%。但现在 table 写的是 5 (83.3%)。这说明这里不仅 denominator 不一致，numerator 也需要核对，不能只把所有百分比的分母换一下就算完成。

同样，Placebo 的 Gastrointestinal disorders 和 Nausea，在 safety population 里各涉及一个 subject，应该是 1 (20.0%)，而 table 都写成了 2 (33.3%)。另外，spec 还规定 SOC 按字母排序，SOC 里面的 PT 按跨 treatment group 的 subject 总数降序排列，同数再按字母排。因此 Nervous system disorders 下面，Headache 应该放在 Dizziness 前面。

这些就是我们需要写给 AI 的 Rules：选哪个 population、在哪个层级数 subject、用什么 denominator、保留几位小数，以及按照什么规则排序。log 也要看。这里 log 已经提示 Placebo denominator 是在 SAFFL filter 之前生成的，但具体代码怎么改、其他 count 的差异怎么造成，仍然需要 programmer 检查源码，并通过 rerun 确认，不能直接把所有问题都归到一个原因上。

最后是 Output。我们希望拿到的就不只是“可能有问题”，而是一张 review table：finding 是什么，severity 怎么判断，evidence 在哪里，current value 和 corrected value 分别是多少，影响哪些 rows，以及 next step 是什么。比如刚才 Any AE 那一行，就可以写清楚：当前 5 (83.3%)，独立重算为 4 (80.0%)，依据是 ADSL、ADAE 和 spec；下一步请 programmer 核对 population 和 counting logic，修正后重新生成 table，再做 QC。

所以我们看右边这个完整 prompt，其实任务没有变，还是 review 同一张 AE table。变化在于，我们把刚才实际用到的文件角色、统计规则和交付要求写出来了。这样 AI 才有一个明确的标准去执行，我们也有一个标准去检查它的结果。

## Page 5｜Align Before Execute

但真正接到任务的时候，我们可能还没有把刚才这些东西全部想清楚。所以这页讲的是，如果手里只有一个 rough idea，怎么一步一步把它变成刚才那个 prompt。

先看左边这些 common problems。还是这个 AE case，如果 AI 只说“有一些 Placebo issues”，那结果太 generic，我们就要求它列出具体 row、current value 和 corrected value。如果拿到的是一大段文字，格式不方便 review，就给它 Finding、Evidence、Correction、Next Step 这样的 output schema。如果是给 Leader 看，我们可以要求先讲最重要的 finding，计算细节放到后面。每次都针对一个具体问题修改，而不是只说“再好一点”。

中间是更早一步：连我们自己都还不确定缺什么的时候，可以先让 AI 帮忙整理需求。比如我只有那五个文件和 Leader 的一句话，就先告诉它：“Please do not execute this task directly.”先检查我的任务有没有缺 background、input、rules、output format 或 validation criteria，再问最多三个最重要的问题。

放到这个 case 里面，值得先澄清的可能就是：这次需要独立重算所有 n (%)，还是只做表面一致性检查？统计规则以哪个版本的 spec 为准？最后需要一段 summary，还是逐项可处理的 QC issue list？这些是我们可以要求 AI 检查的问题，不是说 AI 已经在这次对话里实际问过了。文件里已经明确的规则，也应该先读取，不需要再让人重复提供。

右边是当 prompt 基本明确以后，执行前再对齐一次。我们可以让 AI 先说它准备怎么做：先读 spec；再用 ADSL 确认 SAFFL=Y 的 safety denominator；用 ADAE 按 subject 重算 Any AE、SOC 和 PT；然后和 RTF 逐行对照，检查百分比、排序及 log warning，最后生成 issue list。

如果它在这一步说“我准备直接统计 ADAE 的记录数”，我们就能在执行之前发现它把 event count 和 subject count 混淆了。现在纠正，只需要明确一句“按 distinct subject 统计”；等整张表都算完再改，就要重新走一遍。

所以我们不需要一开始就写出一个完美的 prompt。上面这五步 Define → Generate → Review → Refine → Reuse，就是先定义任务，形成第一版，再拿具体结果来检查和修正。等到这个 AE review 的输入、规则和输出结构稳定了，再把做得好的部分保存成 template，下次换一组文件继续用。

到这里，我们先解决了怎么让 AI 知道要做什么。但当后面开始反复上传文件、修改要求、追问结果时，它现在到底在参考哪一份信息？这就是下一段要讲的 Context。

## Page 6｜Context — AI Responds to More Than Your Last Message

随着任务越来越复杂、对话越来越长，我们会不断加入新的文件、新的信息、新的要求，甚至不断修改前面的要求。我们的整个 conversation 还是可能越来越 messy。这里还有就会出现一个很常见的问题：Prompt 已经清楚了，为什么随着文件、修改和对话越来越多，AI 又开始忘记要求、使用旧版本，甚至越聊越乱？这其实就和 Context 有关。

我们先看一个很简单的例子。现在我们只对 AI 说了一句“Make the summary shorter.”从我们的角度看，这个 Prompt 非常短，好像只有几个词。但 AI 在回答这句话的时候，它看到的通常不只是这几个词。它可能还在处理前面的 System Instructions、最开始的 Original Task、之前的Conversation History、我们上传过的Files、它前面生成的 Outputs、我们后来乡它的 Corrections，甚至还有 Tool Results 和现在最新的 Requirements。

所以说一个短的input 并不意味着一个小的 small context。我们输入的可能只有一句话，但它实际上是放在一个更大的 Context 里面被理解的。AI 会基于当前系统提供给它的 Context 来回答，而不同的产品，也可能通过不同的方式去保留、检索、总结或者截断之前的历史信息。这也意味着，当任务越来越长的时候，我们真正需要管理的已经不只是 Prompt 本身了。这也是为什么我们经常感觉到还没有怎么使用github copilot就token消耗很快的原因。

问题开始从“How do we write a better prompt?”变成“How do we manage context before it becomes messy?”

## Page 7｜How Context Gets Polluted

其实很多时候，Context 是在正常工作的过程中一点一点变乱的。最开始任务可能很简单，比如 “Summarize current project risks.” 但随着任务推进，我们会不断补充新的要求，中间还可能穿插其他任务。到了 Round 21，我们只说一句 “Go back to the summary and revise it.”

对我们来说，现在要什么其实很清楚。但对 AI 来说，整个 conversation 里可能同时存在旧要求、新要求、不同版本的文件、已经被推翻的决定、无关的讨论，以及大量中间输出。

于是我们就会看到这些问题：已经删掉的 Budget 又回来了；上传了今天的文件，却又用了上周的版本；前面要求 one-page，聊了十几轮以后这个限制消失了。

所以很多时候，问题并不是 lack of information。恰恰相反，是信息很多，但真正重要的信息不够 prominent。那 Context Management 实际可以做什么？这页我把它归纳成四个动作。

第一，Remove：把已经过时的要求、旧文件、被否决的方案和无关内容移出去。

第二，Resolve：如果两个要求互相冲突，不要让两个版本一直并存，要明确现在的 source of truth 是什么。

第三，Compress：把很长的历史讨论压缩成一个结构化的 Working Context，而不是让 AI 每次重新理解几十轮对话。

最后是 Retrieve：不是所有东西都要一直塞在 Context 里面。真正需要的时候，再把相关文件或者信息拿进来。

Context Engineering 的重点不是怎么把所有信息都给 AI，而是“怎么确保 AI 在正确的时间看到正确的信息。我们管理的不只是 Prompt，而是 AI 工作的整个信息环境。

## Page 8｜The Context Reset Protocol

如果 Context 已经变得很 messy 了，那我们可以用一个简单的很简单的 STOP method。首先Stop，不要在已经很乱的 conversation 里面继续加新的要求，然后 Take Stock，看一下我们现在的目标是什么、已经做到哪里、还有什么问题。接下来 Organize，把现在仍然有效的信息、已经过时的信息，以及还没有决定的问题分开。最后再 Proceed Cleanly，用一个干净的 Structured Handoff 继续工作。

下面就是一个例子。前面可能已经聊了 21 轮，用过 3 个版本的数据，改过 5 次要求，中间还穿插了其他问题。这个时候与其让 AI 自己从几千字的 conversation 里面判断什么还有效，不如直接重新整理当前状态。

比如这里我们只保留六件事现在的 Goal 是什么，Current State 到哪里了，哪些 Decisions 已经确定，哪些 Open Issues 还没有决定，哪些旧信息需要 Ignore，以及 Next Step 是什么。

这里我觉得 Open Issues 和 Ignore 特别重要。因为 Context Management 不只是告诉 AI “你要记住什么”，还要告诉它什么已经决定了，什么还没有决定，以及什么已经失效尤其是 Open Issues 很有价值。因为 AI 一个很常见的问题不是“忘记信息”，而是会把尚未决定的事情自动补成一个决定。

当然，这个 Structured Handoff 更多是在我们已经发现 Context 变 messy 之后做的一次 reset。对于真正复杂、周期比较长的任务，其实没必要等到 Round 21 才来整理。我们完全可以从一开始就建立一个类似的 memory.md，持续记录当前进度、已经做出的决定、Open Issues 和 Next Step，让它成为任务的动态状态。

所以 Context Reset 并不是简单地“总结一下之前聊了什么”。它真正要做的是把历史 conversation 转换成当前任务真正需要继续的 state。

如果是一个长期项目，我们当然也可以把这种 Structured Handoff 保存下来，持续更新。但核心原则不变稳定的信息单独维护，变化的状态持续更新，不要把整个聊天记录当成唯一的 memory。

## Page 9

前面我们解决了 Prompt 和 Context 的问题，但即使 AI 用对了信息，最后还有一个很实际的问题，就是它的 Output 到底好不好用。我们经常会觉得 AI 写得太长、太啰嗦，但很多时候，问题不只是字太多，而是它不知道这些信息最后是给谁看的。

比如上面这个例子，AI review AE summary 以后发现 Placebo group 的 denominator 有问题。它把问题本身、program 要检查什么、统计上需要确认什么，以及这个问题会不会影响最终 deliverable，全部写在了一段话里面。这些信息本身可能都有用，但不同角色关心的层级其实不一样。

Output Design 的核心不是简单地让 AI “写短一点”，而是根据使用者重新组织 information hierarchy。通过这个Output Contract就是把这件事情提前定义Audience、Purpose、Priority、Format、Length，这样 AI 才知道什么应该放在最前面，什么可以简化，什么甚至可以直接省略。

当然如果已经拿到一个很长的 Output，也可以用下面这个 Output Repair Prompt，让 AI 保留已经验证过的结果，只重新组织内容，而不是重新做 analysis。所以我们真正需要的不是单纯 shorter，而是对正确的人，提供正确层级的信息。

## Page 10

但是 usable 不等于 reliable。那 Output 看起来清楚以后，还有一个更重要的问题，就是这些结论到底能不能相信。比如这里，我们从 Table 里面看到 denominator 是 40，而从 analysis dataset 里面确认符合 analysis population 的是 38。那我们能够确定的 Fact 其实只有一个，就是这里存在 denominator inconsistency。但 AI 很容易继续往下推一步，比如说，“这个问题是因为 program 用错了 population filter。”这个解释听起来非常合理，但问题是，我们现在的文件并没有直接证明这一点。

所以我觉得这里一个很实用的方法，就是要求 AI 把自己的 key claims 分成三类Fact、Inference 和 Unknown。我们可以直接把这个规则放进 Prompt，让 AI 在输出结果以后，再做一次 Evidence Check。Fact 要告诉我 Evidence 在哪里，Inference 要告诉我还缺什么验证，证据不足的就保留为 Unknown，不要自己补成一个 Conclusion。

当然，这并不是说 AI 给自己标了一个 Fact，我们就可以直接相信。真正的作用是让它把 Claim 和 Evidence 之间的关系显式地展示出来，这样我们才能回到 source 去验证，也能更快发现 AI 是在哪一步从 Evidence 跳到了 Assumption。

Structured Prompt 决定 AI 知不知道该做什么；Managed Context 决定 AI 有没有看到正确的信息；Verifiable Output 决定我们能不能知道它的结论从哪里来。

这三个放在一起，i才开始从简单的 Chatting with AI，变成意义上的 Working with AI的第一个步骤。
