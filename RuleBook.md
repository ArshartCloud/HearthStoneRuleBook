Sequences, Phases, Queues, Resolution
流程、时点、队列、处理
Definition: Player Actions are actions a player chooses to take on their turn while nothing is happening, such as attacking, playing a card, using your Hero Power and ending your turn.
定义：玩家动作是玩家在空闲点能发起的动作，如攻击，使用一张牌，使用英雄技能及结束回合。
Definition: A Sequence is what begins when a Player Action is taken. A Sequence consists of one or more Phases, that are resolved in order.
定义：流程是从玩家动作作为开始产生的一系列结算步骤。一个流程包含一个或多个依次处理的时点。
Definition: Phases are surrounding blocks created whenever one or more triggers/Events are raised. When the outermost Phase resolves, Hearthstone will run several Steps, including processing Deaths and updating Auras.
定义：时点是当一个或更多的触发技/事件发起的时候创造的环绕区间。当最外层的时点处理完毕，炉石传说会发起一些步骤，包括死亡处理和光环更新。
Hearthstone splits Turns into Sequences.
炉石传说将回合分为若干流程。
Player Actions (such as Combat, playing a card and ending the turn) form a Sequence of one or more Phases.
玩家动作（例如战斗，使用牌，结束回合）会形成一个有一个或多个时点的流程。
Examples
例如
Sending a Character to attack another character creates a Sequence of two Phases - "Preparation" and "Attack".
让一个角色攻击另一个角色会创造一个拥有两个时点-“准备”和“攻击”的流程。
Whenever a minion is summoned, a Sequence immediately begins with an "On Summon" and ends with an "After Summon" Phase.
当一个随从被召唤时，会创造一个从“召唤时”开始到“召唤后”结束的流程。 

Definition: An Event is any change in the game state. For example: Damage Event, Heal Event, Death Event, etc. (Additionally, all Phases have an associated Event(s).)
定义：一个事件是指游戏状态的任意改变。例如：伤害事件，治疗事件，死亡事件，等等（额外地，所有时点都有相联系的事件）。
Definition: A Trigger is something that reacts to an Event, i.e. triggered effects, Secrets and Deathrattles.
定义：一个触发技是指一些对事件的响应，如，触发效果，奥秘，亡语等。
Definition: Resolving means playing out all related consequences, one at a time.
定义：处理意为完成所有相关的结果，一次一个。
Rule 1a: A Phase, trigger or Event is only resolved when all of its consequences are resolved.
规则1a：一个时点，触发技或事件仅当它们所有的结果被处理后才算被处理完。
Rule 1b: When resolving simultaneous events, Hearthstone must resolveone event before it begins resolving the next.
规则1b:当处理复数事件时，炉石传说必须在处理下一个之前先处理完第一个。
Rule 1c: Death and Auras are not checked during the standard resolution of Events.
规则1c：死亡和光环不会在标准的处理事件中检查。

 
The process of resolving an event is similar to a depth-first search - Imagine every circle being an event and every arrow representing a trigger starting a new event. The numbers on each circle are the order Hearthstonewould resolve them in.
处理一个事件的过程类似于深度优先搜索-想像每个圆是一个事件且每个箭头代表触发一个新的事件。每个圆的数字代表炉石将会处理它们的顺序。
When multiple events are awaiting resolution, the need to resolve an event before starting the next is a depth-first resolution. (If multiple events could be partially resolved, that would be breadth-first).
当复数事件等待处理时，要在处理下一个事件前先处理前一个的是深度优先处理。（如果多个事件能局部解决，那将是广度优先）
The moment a new trigger/Event is raised, Hearthstone begins to resolve it and immediately begins exploring its consequences, before resolving those remaining for the current trigger/Event. When a trigger/Event isresolved,Hearthstone picks up where it left off.
 当一个新的触发技/事件发生时，炉石传说会先处理它并在处理那些还在等待的触发技/事件前，先展开它的结果，当一个触发技/事件被处理后，炉石会从它原先的地方继续结算。
Examples
You Flamestrike a Dragon Egg and Knife Juggler. The Dragon Egg immediately spawns a Black Whelp, causing the Knife Juggler to trigger and throw a knife (even though both are mortally wounded, because death is not checked during resolution). There are no further consequences, so the phase is resolved. Hearthstone kills both minions, removing them from the board.
你对一个龙卵和飞刀杂耍者使用烈焰风暴。龙卵会立刻召唤一个黑色雏龙，导致飞刀杂耍者触发并掷出一把刀(即使它们都受到致命伤，因为在处理时并不会检查死亡）由于没有更多的结果，所以时点处理完毕。炉石杀死所有随从，从场上移除它们。
