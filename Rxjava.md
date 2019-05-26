# RxJava #

http://reactivex.io/documentation/operators.html#utility
https://blog.csdn.net/henreash/article/details/83477611

## 介绍
每种特定语言都有一组ReactiveX操作符,虽然这之间有太多重叠的实现,但是也有一些操作符有特定的实现.另外,每个操作符的实现,命名尽量采用该语言已有或相似的方式.

## 链式操作符
绝大多数的链式操作符使用Observable调用,并返回一个Observable对象,这允许你在一个操作符后,继续调用下一个操作符.在一个链中,链上的每个操作符修改的Observable都是前一个操作符的操作结果。

有一种模式，像建造者模式，为类提供了各种方法来修改对象数据成员。这个模式可同样实现类似的方法链。在建造者模式中，方法的调用顺序不影响最终结果，但Observable操作符是顺序敏感的。

链中的Observable操作符不是直接针对原始的Observable对象，相反，每个操作符操作的Observable都是链上前一个操作符的操作结果。

### ReactiveX操作符
本页的第一个列表是ReactiveX的核心操作符，链接页面描述操作符使用的详细信息及特定语言版本的情况。

第二个列表是决策树，帮助用户根据自己的用例选择操作符。

最后以字母顺序排列了所有ReactiveX语言版本实现的操作符。链接指向近似语言实现版本的操作符描述文档（例如，Rx.net的SelectMany操作符链接到ReactiveX的FlatMap操作符文档，SelectMany是其Rx.net的实现）。

如果想实现自定义的操作符，请见 Implementing Your Own Operators.

目录Contents

1.操作符目录（Operators By Category）
2.Observable操作符决策树（A Decision Tree of Observable Operators）
3.按字母排序的Observable操作符（An Alphabetical List of Observable Operators）

### 一.操作符目录
1.创建一个新的Observable对象。

```
Create ----用手动触发观察者的方式来创建一个Observable对象（链接中描述了如何在自定义方法中触发订阅、完成通知）

Defer ----等待观察者订阅时才会创建Observable对象，为每个观察者创建一个新的Observable

Empty/Never/Throw ---- 创建具有特定限制行为的Observable

From ----将其他对象或数据结构转换为Observable对象

Interval ---- 创建一个指定时间间隔发送自增整数序列的Observable。

Just---- 将对象或一系列对象转换为发送这个对象或对象序列的Observable。

Range ---- 创建发送一系列整数的Observable

Repeat ---- 创建一个Observable对象重复发送特定数据项或数据项序列

Start ---- 创建一个发送函数返回值的Observable

Timer ---- 创建指定时间间隔发送一个数据项的Observable
```

2.Observable变换 : 变换Observable发送的数据项的操作符

```
Buffer — 周期性的收集Observable发送的数据，存入到缓冲区后统一发送，而不是收到一个发送一个

FlatMap — 将一个Observable发送的数据项变换为Observable集合，在将Observable集合发送的数据项合并得到另一个Observable

GroupBy — 将一个Observable对象拆分为多个Observable，源Observable发送的数据项按key值分组到特定Observable上进行发送

Map — 将Observable发送的数据项应用变换后得到新的Observable

Scan — 将Observable发送的数据项使用函数按顺序计算后，发送结果数值

Window — 周期性的将Observable对象发送的数据项分组，统一发送这个窗口期的数据项，而不是接收一个数据项发送一个数据项
```
3.过滤Observable （Filtering Observables）:选择从源Observable对象发送数据项的操作

```
Debounce — 去抖动，Observable发送数据项，如果在指定时间段内发送过，则拦截掉

Distinct — 对Observable发送的数据项去重

ElementAt — 仅发送Observable发送数据项的顺序号

Filter — 仅发送通过谓词检测的Observable发送的数据项

First — 仅发送Observable发送的第一个数据项，或符合条件的第一个数据项

IgnoreElements — 拦截Observable发送的所有数据项，但会发送结束通知

Last — 仅发送Observable发送的最后数据项

Sample — 采样 在指定时间间隔内发送一个Observable最新的数据项

Skip — 拦截Observable发送的前N个数据项

SkipLast — 拦截Observable发送的最后N个数据项

Take — 仅发送Observable发送的前N个数据项

TakeLast — 仅发送Observable发送的最后N个数据项
```

4.组合Observable（Combining Observables）:将多个Observable组合为一个Observable的操作符

```
And/Then/When — 根据特定模式和计划将多个Observable发送的数据项合并为一个

CombineLatest — 当多个Observable有一个发送了数据项，将这些Observable发送的最新的数据项使用特定函数进行组合，而后发送出去

Join — 将两个Observable对象发送的数据项进行组合，要求一个Observable对象发送数据项必须在另一个Observable发送数据项的时间窗内

Merge — 将多个Observable发送数据项合并到一个Observable中

StartWith — 在源Observable发送数据项前先发送一个特定数据序列

Switch — 将发送Observable对象的Observable转换为单个Observable，发送源Observable最近发送的数据项

Zip — 将多个Observable发送的数据项通过函数组合成为一个单独的数据项，并进行发送
```
5.错误处理操作符（Error Handling Operators）:帮助捕获Observable错误通知的操作符
```
Catch — 捕获onError通知并继续执行

Retry — 如果源Observable发送了onError通知，为无错误继续执行进行重新订阅
```
6.Observable公共操作符:对Observable有益的一组操作符
```
Delay — 将Observable发送数据项沿时间轴向前移动

Do — 注册Observable各种生命周期事件处理函数

Materialize/Dematerialize — 将数据项发送和通知合并为数据项发送，或相反操作

ObserveOn — 给Observable的观察者指定Scheduler（订阅函数执行的线程）

Serialize — 强制Observable按顺序调用订阅，接口友好

Subscribe — 给Observable指定发送数据项和通知的处理函数

SubscribeOn — 指定Observable在处理订阅时的Scheduler上下文

TimeInterval — 将Observable转换为发送带有时间段（从开始发送到当前项的时间段）数据项的Observable

Timeout — 源Observable的镜像，如果源Observable在指定时间内没有发送数据项则发送错误通知

Timestamp — 将时间戳附加到Observable发送的数据项上

Using — 创建与Observable相同生命周期的可释放资源（IDisposable类型）
```

7.条件和布尔操作符: 评估一或多个Observable或其发送的数据项
```
All — 判断Observable发送的所有数据项是否都遵守相同的规则

Amb — 在多个Observable中仅发送第一个发送数据的Observable发送的数据项

Contains — 判断Observable是否发送特定了数据项

DefaultIfEmpty — 发送源Observable发送的数据项，如果源Observable没有发送数据项则发送默认项

SequenceEqual — 判断两个Observable是否发送了相同的序列

SkipUntil — 在第二个Observable发送数据项前，抛弃第一个Observable发送的数据项

SkipWhile — 当特定条件成立则抛弃Observable发送的数据项

TakeUntil — 在第二个Observable发送数据项或中止之后，抛弃第一个Observable发送的数据项

TakeWhile — 当特定条件不成立则抛弃Observable发送的数据项
```

8.数学和统计运算符:操作Observable发送的数据序列的操作符
```
Average — 计算Observable发送的数据项的平均值，并发送这个平均值

Concat — 无交叉的合并多个Observable发送的数据项并发送出去

Count — 计算源Observable对象发送的数据项数量，并发送

Max — 计算Observable发送的数据项最大值，并发送

Min — 计算Observable发送的数据项最小值，并发送

Reduce — 对Observable发送的数据项应用一个函数，并按顺序发送结果值

Sum — 计算Obsrvable发送的数据项的和，并发送
```

9.反压操作符（Backpressure Operators）
```
backpressure operators — 解决Observable发送数据项速度比观察者处理速度快的应对机制（生产者速度快，消费者速度慢）
```

10.Observable连接操作符:可以精确控制动态订阅的特殊Observable
```
Connect — 指示可连接的Observable开始向订阅者发送数据项

Publish — 将普通的Observable转换为可连接Obsrevable

RefCount — 将可连接Observable转换为普通Observable

Replay — 保证所有观察者可以收到同样的数据序列，即使订阅时机比开始发送数据项晚（可以补发已发送过的数据项）
```

### 二.Observable操作符决策树

1.需要创建一个新的Observable对象
```
发送特定数据项（that emits a particular item） ---- Just

以函数为参数，订阅时才执行（that was returned from a function called at subscribe-time）---- Start

以Action、Callback、Runable等类似的对象为参数，订阅时才执行（that was returned from an Action, Callable, Runnable, or something of that sort, called at subscribe-time）---- From

在指定的延时后执行（after a specified delay） ---- Timer

从Array、Iterable等类似对象中获取数据项并发送（that pulls its emissions from a particular Array, Iterable, or something like that）----  From

从Future对象转换（by retrieving it from a Future）---- Start

从Future对象获取序列（that obtains its sequence from a Future）---- From

重复发送序列中的数据项（that emits a sequence of items repeatedly）---- Repeat

自定义逻辑（from scratch, with custom logic 可用代码调用onNext、onComplete决定发送数据项内容和时机）---- Create

等待所有订阅的观察者（才发送数据项）（for each observer that subscribes）---- Defer

发送一系列连续的整数（that emits a sequence of integers）---- Range

指定时间间隔发送数据项（at particular intervals of time） ----  Interval

指定时间间隔后发送数据项（after a specified delay）---- Timer

不发送数据项即结束（that completes without emitting items） ---- Empty

什么也不做 （that does nothing at all） ---- Never
```

2.通过组合其他Observable创建Observable（I want to create an Observable by combining other Observables）
```
按发送时间顺序组合多个Observable发送的数据项（and emitting all of the items from all of the Observables in whatever order they are received）---- Merge

按Observable的顺序组合多个Observable发送的数据项（ and emitting all of the items from all of the Observables, one Observable at a time）---- Concat

组合多个Observable发送的数据项为新的数据项，每个Observable发送的数据项的时候都会触发这种操作（by combining the items from two or more Observables sequentially to come up with new items to emit whenever each of the Observables has emitted a new item）---- Zip

当所有Observable都发送了新的数据项时发送组合的数据项（whenever any of the Observables has emitted a new item）---- CombineLatest

一个Observable在另一个Observable发送的数据项决定的时间窗口内发送数据项时被触发（ whenever an item is emitted by one Observable in a window defined by an item emitted by another）---- Join

基于模式和计划的中间对象（by means of Pattern and Plan intermediaries） ---- And/Then/When

仅发送多个Observable对象中最后发送的那个数据项（and emitting the items from only the most-recently emitted of those Observables）---- Switch
```

3.需要将Observable发送的数据项进行变换（I want to emit the items from an Observable after transforming them）
```
每次执行一次函数（one at a time with a function）---- Map

将相应的Observable对象发送的所有数据项发送出去（by emitting all of the items emitted by corresponding Observables）----FlatMap

一次发送Observable全部的数据项（one Observable at a time, in the order they are emitted）---- ConcatMap

基于之前的所有数据项（based on all of the items that preceded them） ---- Scan

给数据项附加时间戳（by attaching a timestamp to them） ---- Timestamp

指示发送数据项前的失效时间（into an indicator of the amount of time that lapsed before the emission of the item）----TimeInterval
```

4.需要将Observable发送的数据项沿时间轴迁移后再次发送（I want to shift the items emitted by an Observable forward in time before reemitting them）---- Delay

5.将Observable发送的数据项和通知转为数据项后再次发送（I want to transform items and notifications from an Observable into items and reemit them） 
```
将其封装为通知对象（by wrapping them in Notification objects）---- Materialize

恢复为原始对象（which I can then unwrap again with）---- Dematerialize
```

6.忽略Observable发送的所有数据项，仅转发其完成和错误通知（I want to ignore all items emitted by an Observable and only pass along its completed/error notification）---- IgnoreElements

7.给Observable发送数据序列加上一个前缀（I want to mirror an Observable but prefix items to its sequence）---- StartWith
```
仅当序列为空（only if its sequence is empty）---- DefaultIfEmpty
```

8.将Observable发送的数据项收集到缓冲区中，作为缓冲区项发送（I want to collect items from an Observable and reemit them as buffers of items）---- Buffer
```
仅包含最后发送的数据项（containing only the last items emitted）---- TakeLastBuffer
```

9.将一个Observable拆分为多个Observable（I want to split one Observable into multiple Observables）---- Window
```
将相似的数据项分配到同一个Observable（so that similar items end up on the same Observable）---- GroupBy
```

10.获取Observable发送数据项的特定项（I want to retrieve a particular item emitted by an Observable）:
```
结束前最后发送的数据项（the last item emitted before it completed） ----  Last

只发送一个数据项（the sole item it emitted） ----  Single

发送的第一个数据项（the first item it emitted）---- First
```

11.仅发送Obsrvable发送的某些数据项（I want to reemit only certain items from an Observable）
```
筛选出不匹配谓词的项（by filtering out those that do not match some predicate）---- Filter

第一项（that is, only the first item）---- First

第一批（that is, only the first items）---- Take

最后一项（that is, only the last item）---- Last

仅序号（that is, only item n）---- ElementAt

忽略前N项（that is, only those items after the first items；that is, after the first n items） ---- Skip

忽略直到匹配谓词的项为止（that is, until one of those items matches a predicate）---- SkipWhile

忽略初始时间段之后的项（that is, after an initial period of time） ---- Skip

忽略第二个Observable发送数据项之前的项（that is, after a second Observable emits an item）---- SkipUntil

忽略最后N项或时间段内的项（that is, those items except the last items；that is, except the last n items）---- SkipLast

获取直到匹配位置的项为止（that is, until one of those items matches a predicate）---- TakeWhile

忽略源Observable完成前一段时间内的项（that is, except items emitted during a period of time before the source completes）----SkipLast

忽略第二个Observable发送数据项后发送的数据项（that is, except items emitted after a second Observable emits an item）----TakeUntil

Observable周期性采样（by sampling the Observable periodically）---- Sample

仅发送小段时间内没有出现的项（防抖）（by only emitting items that are not followed by other items within some duration）----Debounce

去重（by suppressing items that are duplicates of already-emitted items）---- Distinct

去除连续的重复值（if they immediately follow the item they are duplicates of）---- DistinctUntilChanged

开始发送数据项后延迟订阅（by delaying my subscription to it for some time after it begins emitting items）----DelaySubscription
```

12.将Observabe集合中第一个发送数据的Observable发送的数据项发送出去（I want to reemit items from an Observable only on condition that it was the first of a collection of Observables to emit an item）---- Amb

13.要评估Observable发送的数据项序列（I want to evaluate the entire sequence of items emitted by an Observable）
```
发送bool值指示是否所有的数据项都通过测试（and emit a single boolean indicating if all of the items pass some test）---- All

发送bool值指示Observable是否发送了指定的值（and emit a single boolean indicating if the Observable emitted any item (that passes some test)） ----  Contains

返回bool值指示Observable没有发生过数据项（and emit a single boolean indicating if the Observable emitted no items）---- IsEmpty

返回bool值指示两个Observable发送的数据项相等（and emit a single boolean indicating if the sequence is identical to one emitted by a second Observable）---- SequenceEqual

发送所有数据项的平均值（and emit the average of all of their values）---- Average

发送所有数据项的和（and emit the sum of all of their values）---- Sum

发送所有数据项的个数（and emit a number indicating how many items were in the sequence）---- Count

发送数据项的最大值（and emit the item with the maximum value）---- Max

发送数据项的最小值（and emit the item with the minimum value）---- Min

针对每个数据项应用统计函数，发送计算结果（by applying an aggregation function to each item in turn and emitting the result）---- Scan
```

14.将Observable发送的数据项序列转换为其他数据结构（I want to convert the entire sequence of items emitted by an Observable into some other data structure）---- To

15.将操作符切换到特定Scheduler（I want an operator to operate on a particular Scheduler）---- SubscribeOn
```
获取通知（when it notifies observers） ---- ObserveOn
```
16.当Obervable触发特定事件时执行特定操作（I want an Observable to invoke a particular action when certain events occur）---- Do

17.让Observable通知观察者发生了错误（I want an Observable that will notify observers of an error）---- Throw
```
在特定时间段内没有发送数据项（if a specified period of time elapses without it emitting an item）---- Timeout
```

18.Observable容错（I want an Observable to recover gracefully）
```
超时后切换到备份Obervable（from a timeout by switching to a backup Observable）---- Timeout

拦截错误通知（from an upstream error notification）---- Catch

尝试重新执行订阅（by attempting to resubscribe to the upstream Observable）---- Retry
```

19.创建一个与Observable相同生命周期的资源（I want to create a resource that has the same lifespan as the Observable）---- Using

20.要订阅一个Observable对象，并获取等待Observable完成的Future对象（I want to subscribe to an Observable and receive a Future that blocks until the Observable completes）---- Start

21.获取一个等待全部观察者订阅后才发送数据项的Observable（I want an Observable that does not start emitting items to subscribers until asked）---- Publish
```
仅发送序列的最后一项（and then only emits the last item in its sequence）---- PublishLast

向观察者发送全部数据项，即使订阅时已经开始发送数据（and then emits the complete sequence, even to those who subscribe after the sequence has begun）---- Replay

所有订阅者取消订阅对象释放（but I want it to go away once all of its subscribers unsubscribe）---- RefCount

显示的启动（and then I want to ask it to start）---- Connect
```

### 二.Observable操作符按字母排序
```
Aggregate
All
Amb
ambArray
ambWith
and_
And
Any
apply
as_blocking
asObservable
AssertEqual
asyncAction
asyncFunc
Average
averageDouble
averageFloat
averageInteger
averageLong
blocking
blockingFirst
blockingForEach
blockingIterable
blockingLast
blockingLatest
blockingMostRecent
blockingNext
blockingSingle
blockingSubscribe
Buffer
bufferWithCount
bufferWithTime
bufferWithTimeOrCount
byLine
cache
cacheWithInitialCapacity
case
Cast
Catch
catchError
catchException
collect
collect (RxScala version of Filter)
collectInto
CombineLatest
combineLatestDelayError
combineLatestWith
Concat
concat_all
concatAll
concatArray
concatArrayDelayError
concatArrayEager
concatDelayError
concatEager
concatMap
concatMapDelayError
concatMapEager
concatMapEagerDelayError
concatMapIterable
concatMapObserver
concatMapTo
concatWith
Connect
connect_forever
cons
Contains
controlled
Count
countLong
Create
cycle
Debounce
decode
DefaultIfEmpty
Defer
deferFuture
Delay
delaySubscription
delayWithSelector
Dematerialize
Distinct
distinctKey
distinctUntilChanged
distinctUntilKeyChanged
Do
doAction
doAfterTerminate
doOnComplete
doOnCompleted
doOnDispose
doOnEach
doOnError
doOnLifecycle
doOnNext
doOnRequest
doOnSubscribe
doOnTerminate
doOnUnsubscribe
doseq
doWhile
drop
dropRight
dropUntil
dropWhile
ElementAt
ElementAtOrDefault
Empty
emptyObservable
empty?
encode
ensures
error
every
exclusive
exists
expand
failWith
Filter
filterNot
Finally
finallyAction
finallyDo
find
findIndex
First
firstElement
FirstOrDefault
firstOrElse
FlatMap
flatMapFirst
flatMapIterable
flatMapIterableWith
flatMapLatest
flatMapObserver
flatMapWith
flatMapWithMaxConcurrent
flat_map_with_index
flatten
flattenDelayError
foldl
foldLeft
for
forall
ForEach
forEachFuture
forEachWhile
forIn
forkJoin
From
fromAction
fromArray
FromAsyncPattern
fromCallable
fromCallback
FromEvent
FromEventPattern
fromFunc0
fromFuture
fromIterable
fromIterator
from_list
fromNodeCallback
fromPromise
fromPublisher
fromRunnable
Generate
generateWithAbsoluteTime
generateWithRelativeTime
generator
GetEnumerator
getIterator
GroupBy
GroupByUntil
GroupJoin
head
headOption
headOrElse
if
ifThen
IgnoreElements
indexOf
interleave
interpose
Interval
intervalRange
into
isEmpty
items
Join
join (string)
jortSort
jortSortUntil
Just
keep
keep-indexed
Last
lastElement
lastOption
LastOrDefault
lastOrElse
Latest
latest (Rx.rb version of Switch)
length
let
letBind
lift
limit
LongCount
ManySelect
Map
map (RxClojure version of Zip)
MapCat
mapCat (RxClojure version of Zip)
map-indexed
mapTo
mapWithIndex
Materialize
Max
MaxBy
Merge
mergeAll
mergeArray
mergeArrayDelayError
merge_concurrent
mergeDelayError
mergeObservable
mergeWith
Min
MinBy
MostRecent
Multicast
multicastWithSelector
nest
Never
Next
Next (BlockingObservable version)
none
nonEmpty
nth
ObserveOn
ObserveOnDispatcher
observeSingleOn
of
of_array
ofArrayChanges
of_enumerable
of_enumerator
ofObjectChanges
OfType
ofWithScheduler
onBackpressureBlock
onBackpressureBuffer
onBackpressureDrop
OnErrorResumeNext
onErrorReturn
onErrorReturnItem
onExceptionResumeNext
onTerminateDetach
orElse
pairs
pairwise
partition
partition-all
pausable
pausableBuffered
pluck
product
Publish
PublishLast
publish_synchronized
publishValue
raise_error
Range
Reduce
reduceWith
reductions
RefCount
Repeat
repeat_infinitely
repeatUntil
repeatWhen
Replay
rescue_error
rest
Retry
retry_infinitely
retryUntil
retryWhen
Return
returnElement
returnValue
runAsync
safeSubscribe
Sample
Scan
scanWith
scope
Select (alternate name of Map)
select (alternate name of Filter)
selectConcat
selectConcatObserver
SelectMany
selectManyObserver
select_switch
selectSwitch
selectSwitchFirst
selectWithMaxConcurrent
select_with_index
seq
SequenceEqual
sequence_eql?
SequenceEqualWith
Serialize
share
shareReplay
shareValue
Single
singleElement
SingleOrDefault
singleOption
singleOrElse
size
Skip
SkipLast
skipLastWithTime
SkipUntil
skipUntilWithTime
SkipWhile
skipWhileWithIndex
skip_with_time
slice
sliding
slidingBuffer
some
sort
sorted
sort-by
sorted-list-by
split
split-with
Start
startAsync
startFuture
StartWith
startWithArray
stringConcat
stopAndWait
subscribe
subscribeActual
SubscribeOn
SubscribeOnDispatcher
subscribeOnCompleted
subscribeOnError
subscribeOnNext
subscribeWith
Sum
sumDouble
sumFloat
sumInteger
sumLong
Switch
switchCase
switchIfEmpty
switchLatest
switchMap
switchMapDelayError
switchOnNext
switchOnNextDelayError
Synchronize
Take
take_with_time
takeFirst
TakeLast
takeLastBuffer
takeLastBufferWithTime
takeLastWithTime
takeRight (see also: TakeLast)
TakeUntil
takeUntilWithTime
TakeWhile
takeWhileWithIndex
tail
tap
tapOnCompleted
tapOnError
tapOnNext
Then
thenDo
Throttle
throttleFirst
throttleLast
throttleWithSelector
throttleWithTimeout
Throw
throwError
throwException
TimeInterval
Timeout
timeoutWithSelector
Timer
Timestamp
To
to_a
ToArray
ToAsync
toBlocking
toBuffer
to_dict
ToDictionary
ToEnumerable
ToEvent
ToEventPattern
ToFlowable
ToFuture
to_h
toIndexedSeq
toIterable
toIterator
ToList
ToLookup
toMap
toMultiMap
ToObservable
toSet
toSortedList
toStream
ToTask
toTraversable
toVector
tumbling
tumblingBuffer
unsafeCreate
unsubscribeOn
Using
When
Where
while
whileDo
Window
windowWithCount
windowWithTime
windowWithTimeOrCount
windowed
withFilter
withLatestFrom
Zip
zipArray
zipIterable
zipWith
zipWithIndex
++
+:
:+
```