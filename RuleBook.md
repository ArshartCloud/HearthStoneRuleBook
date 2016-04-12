# Sequences, Phases, Queues, Resolution

# 流程、时点、队列、处理

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
例子

Sending a Character to attack another character creates a Sequence of two Phases - "Preparation" and "Attack".  
让一个角色攻击另一个角色会创造一个拥有两个时点-“准备”和“攻击”的流程。

Whenever a minion is summoned, a Sequence immediately begins with an "On Summon" and ends with an "After Summon" Phase.  
当一个随从被召唤时，会创造一个从“召唤时”开始到“召唤后”结束的流程。

Definition: An Event is any change in the game state. For example: Damage Event, Heal Event, Death Event, etc. (Additionally, all Phases have an associated Event(s).)  
定义：事件是指游戏状态的任意改变。例如：伤害事件，治疗事件，死亡事件，等等（额外地，所有时点都有相联系的事件）。

Definition: A Trigger is something that reacts to an Event, i.e. triggered effects, Secrets and Deathrattles.  
定义：触发技是指一些对事件的响应，如，触发效果，奥秘，亡语等。

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
例子

You Flamestrike a Dragon Egg and Knife Juggler. The Dragon Egg immediately spawns a Black Whelp, causing the Knife Juggler to trigger and throw a knife (even though both are mortally wounded, because death is not checked during resolution). There are no further consequences, so the phase is resolved. Hearthstone kills both minions, removing them from the board.  
你对一个龙卵和飞刀杂耍者使用烈焰风暴。龙卵会立刻召唤一个黑色雏龙，导致飞刀杂耍者触发并掷出一把刀(即使它们都受到致命伤，因为在处理时并不会检查死亡）由于没有更多的结果，所以时点处理完毕。炉石杀死所有随从，从场上移除它们。

Definition: A Queue is a sequential container where multiple simultaneous triggers or Events are held.  
定义：一个队列是存放多个同时点触发技或事件的有序容器。
Rule 2a: When we start to resolve a Phase or Event, A Queue is created and filled with all triggers that can respond, in order of play.  
规则2a：当我们开始处理一个时点或事件时，会创造一个按使用顺序填充所有触发技的队列。
Rule 2b: If multiple events are considered simultaneously (such as damage, healing, Deaths or 'return to hand' effects) they are Queued by order of play, then for each, triggers are Queued by order of play (as per Rule 2a).  
规则2b：如果多个事件会被同时考虑（如伤害，治疗，死亡，或‘回到手牌’效果等）它们会按照使用顺序排列，然后，对于每个事件，触发会按照使用顺序排列（按照规则2a）。
Rule 2c: A Queue becomes immutable once Hearthstone starts to resolve the first entry in it. No new entries can be added to the Queue after this point.  
规则2c：一旦炉石开始解决一个队列的第一个项目，该队列将不可改变。新触发技不能在这个时点后被加入队列。

Order of play means the order the Entities each Event/trigger is associated with entered play, from oldest to newest.  
使用顺序意为与事件/触发技相联系的实体进入游戏的顺序，从最早的到最新的。
Minions, Heroes, Weapons, Secrets, attached Enchantments and added Deathrattles are all Entities, and all exist in the same order of play list together.  
随从，英雄，武器，奥秘，结界和结附的亡语都是实体，都存在于相同的使用顺序列表。  
Minions and Secrets summoned while resolving an Event cannot respond to Events that are in the middle of resolution, because their associated Queues are now immutable. However, they can Queue on any later Phases and Events created.  
在处理一个事件中召唤的随从和奥秘不能在该事件处理中触发效果，因为与此事件相关联的队列已经不可更改。然而，它们能在以后的时点和新生成的事件中加入队列。

Examples:  
例子：  
If you trade your Sylvanas Windrunner into your opponent's, the oldest Sylvanas will have its Deathrattle activate first.  
如果你用你的希尔瓦娜斯·风行者攻击你的对手的希尔瓦娜斯·风行者，旧的希尔瓦娜斯·风行者将会先触发它的亡语。  
If you Arcane Explosion three Grim Patrons and a Frothing Berserker, all the damage occurs, then each "On Damage" Event is resolved based on the order of play.  
如果你对三个恐怖的奴隶主和一个暴乱狂战士使用魔爆术，所有的伤害同时发生，然后每个“受到伤害时”事件会按照随从的使用顺序依次处理。  
If a Mad Scientist dies and plays Duplicate, Duplicate does not get triggered. That Death Event has already begun resolving before the Duplicate entered play. If a second minion also died after Mad Scientist, the Duplicate was in play and thus can trigger.  
如果一个疯狂的科学家死亡且其亡语将复制置入战场，复制将不会触发。此死亡事件在事件进入游戏前已经开始处理。如果第二个随从也在疯狂的科学家后死亡，复制已经进入游戏因此可以触发。  
If you play a spell, Troggzor the Earthinator summons a Burly Rockjaw Trogg. The Burly Rockjaw Trogg does not trigger from the same spell because the consequences of playing the spell have already begun resolving.  
如果你使用一个法术，颤地者特罗格佐耳会召唤一个石腭穴居人壮汉。该石腭穴居人壮汉不会因此法术而触发，因为“使用法术时”已经开始处理。  

Notes and exceptions:  
注意和例外：  
Some triggers have a Priority that supersedes order of play and always triggers earlier or later. One example is Redemption which always Queues last.  
一些触发有自己的优先度取代使用顺序，总是最早或最晚触发。一个例子即救赎总是排列在队尾。  
Baron Rivendare also cannot add additional triggers once a Queue has been populated.   
一旦一个队列已经完成，瑞文戴尔男爵就不能增加额外的触发。  
Mechanics that play a minion from your hand or from your deck have a bug that makes the new minion the oldest, not newest. (For more information, see the Force play section.)  
从你的手上或卡组直接使用一个随从的机制有一些bug会让新的随从变成最老的，而非最新的。（更多信息参阅强制使用章节）

Rule 3: Once a Phase begins, nested Phases with their own Queues may start and end inside of it, but only the outermost Phase ending initiates the Death Creation Step.  
规则3：一旦一个时点开始处理，有着各自队列的嵌套的时点会在其内部开始和结束，但是只有最外层的时点结束后才会开始死亡创造步骤。  

This means that you will NEVER see an Entity be killed in the middle of a Phase, no matter how complexly nested it becomes.  
这意味着你不可能看见一个实体在一个时点中间被杀死，无论嵌套多么复杂。  
This also means that even though Sequences like summoning a minion have many Phases, if it occurs as a consequence of another Player Action instead of being due to playing a card, the entire thing happens before any Deaths occur.  
这也意味着虽然一个流程如召唤一个随从可能包含许多时点，如果它作为结果出现在另一个玩家动作而不是使用牌，这整个流程会在任何死亡发生前处理完。  

Examples:
例子：  
You play Knife Juggler then Dr. Boom. When Dr. Boom's Battlecry (a Phase) begins, Boom Bots are summoned, and each one triggers the Knife Juggler to throw knives at enemy minions. Even though minion summoning is a Sequence of multiple Phases, we are already inside of a Phase, so the entire Battlecry remains inside of one Phase, rather than starting and stopping. Finally when the Battlecry resolves, Deaths are processed and the Deathrattles go off.  
你使用飞刀杂耍者和砰砰博士。当砰砰博士的战吼（一个时点）开始后，砰砰机器人被召唤，然后每个触发飞刀杂耍者向敌方随从掷出飞刀。虽然随从召唤是由多个时点组成的流程，但是这些已经在一个时点里，所以整个战吼持续在一个时点里，而不是开始或结束。最后战吼处理完毕，死亡事件开始生成且亡语开始生效。  
You play three Unstable Ghoul. Your opponent plays an Acolyte of Pain, damages it to 1 Health and casts Flamestrike. All three Unstable Ghouls's Deaths are considered in one Phase, meaning that the Acolyte of Pain is hit, triggered and draws three cards, despite being mortally wounded after the first Deathrattle. Finally the Phase ends and the Acolyte of Pain is killed.  
你使用三个蹒跚的食尸鬼。你的对手使用苦痛侍僧，将它伤害到生命值为1，然后施放烈焰风暴。所有三个蹒跚的食尸鬼的死亡在同一个时点，意味着苦痛侍僧会受到伤害，触发并抽三张牌，尽管它在第一次亡语后已经受了致命伤。最后时点结束，苦痛侍僧被杀死。  
Your opponent has a Cult Master and Novice Engineer both at 1 Health. You play a Mad Bomber, and both are reduced to 0 Health during the Battlecry Phase. Regardless of order of play, and regardless of the order the minions are mortally wounded by the bombs, the Cult Master cannot draw a card from the Novice Engineer dying because both deaths occur simultaneously after the Phase ends.  
你的对手使用一个诅咒教派领袖和工程师学徒都只有1生命值。你使用疯狂投弹者，对方所有随从的生命值在战吼时被减少至0。无论使用顺序如何，诅咒教派领袖都不能因工程师学徒死亡而触发抽牌效果，因为它们在时点结束后同时死亡。  
Exceptions:
例外:
There are three effects in the game that break this rule and kill minions in the middle of a Phase. For more information, see the Forced Death Phase section.  
游戏中有三个效果打破了这条规则而在一个时点中杀死随从。详情参阅强制死亡章节。  
