# July 2024

## 19th July 2024

<p style="color: blue;">Day - 1</p>
Day - 1

## 20th July 2024

### Day - 2

I have woke up at 08:00 am, and have solved some DSA and CP questions.
Now I don't know what to do. I am feeling very indecisive about what
to do. Perhaps I should watch one video of Dr. K.

Since today is a new day, and I am starting this kind of thing from
scratch, I don't really have anything important in my mind.
But I will make some kind of list nonetheless:

- [x] At 06:00 pm, go for some running
- [x] At 08:00 pm, set an alarm for Leetcode contest

I think this much is enough for now. I will make some other changes if needed.

# Day - 3

- Date: 22/06/2024

I haved learnt something new about my brain today

- everything my brain feels, it has been evolved to
  feel so
- the anxiety that I feel does also have a reason, rather than
  ignoring it or trying to avoid my emotion( i.e. anxiety in this case)
  maybe I should try to get under the reason of why am I feeling so
- anxiety I think is a **anticipation mechanism**, through which we
  try to foresee things, and how to make them better in the future
- everything can be made in proper manner, if we split the sitatution
  in suitable easier term to understand
- anytime we have anxious thoughts, our anxious thoughts are always
  about the future
- anything that hurts us physically or mentally, there is a possibillity that our mind can become anxious due to anticipation of that outcome in the future
- and the degree of influence of that hurt or anxiety would depend on the gap between the present circumstance and the future time
- also it depends on the degree of hurt or effect that thing which is missing or goes wrong in the future also affects us
## How to I normally try to deal with anxiety
- Whenever the feeling of anxiety decides to get worse, I try to escape from it from distracting my mind in the present
    1. Some of the ways are I try to watch a some low-effort and entertaining albeit distacting video on youtube many a times the content of the video is not that important to me, as much as keeping my mind away from the anxious thoughts are important
    2. Other times I think of going to other people talk useless shit with them
    3. And there are other ways perhaps I will elaborate about them in the future when I become more aware of the behavior



## Day - 3
- Date - 23/07/2024
Goals for today
- [ ] Read 1 chapter of Golang programming language book
- [ ] Read 1 hour on OOPS
- [ ] Read 1 hour on OS
- [ ] Read DSA theory 1 hour from GFG

## Day - 4
**Date - 30/07/2024**
//
Nothing is really changing, I am doing the same thing everyday with so sign of improvement.
I dont know how to get out of this loop. I started meditation some days ago, but for now
I have stopped practicing it. Who am I waiting for??
I am very very weak in problem solving, I strongly need practice, there are only two choices for
me, whether to be weak in problem solving, or be strong in it. 
I choose the latter.

Some






## Day 5
-  Date 08/08/2024

Human beings have a primal brain, whenever there is any difficult situation
they are facing there parasympathetic nervous system takes over. 
They start seeing things in black & white and they start thinking in black & white.

- Today's Complany Applications
1. DevOps Intern(https://jobs.bureau.id/?ashby_jid=fc951ad0-bdd1-4b36-b354-e3f8964aabda&utm_source=0v66G4vzkn)
  They are looking for a six-months internship in Banglore.
  Must prepare for this one seriously

## Day 6
- Date 20/08/2024
- Today's Company Applications
1. Software Engineer - node/Python
Hyderabad, Telangana (https://dhan.freshteam.com/jobs/_iz9XKgk3VFU/software-engineer-node-python?ft_source=1000108832&ft_medium=1000102594)
2. Your application was sent to Yext!

## Day 7 
This is a new begining for me,as I have stopped wasting time on youtube and I am going to try fully to 
control my other addictions, and I am going to practice meditation whenever I get some break.

### Problems Done
1. DFS shortest path problem( could've improved time complexity by using Dijsktra or Bellman Ford)
2. Maximum Difference (GFG POTD)(made used of monotonically increases stack from left and right hand side)
3. https://neetcode.io/problems/count-connected-components (I finally solved this question from scratch without looking)
4. 

  #   Day 1
2024-10-06

## Problems done today
1. "424. Longest Repeating Character Replacement /leetcode"

You are given a string s and an integer k. You can choose any character of the string 
and change it to any other uppercase English character. You can perform this operation 
at most k times.

Return the length of the longest substring containing the same letter you can get 
after performing the above operations.

So here is my approach, writing as simpler as I can

```
create a hashmap to store frequency of each letter
start = 0, end = 0
store frequency of substring from start to end
```

#  Day 2
2024-10-07
01:04

So call out my name.

## Problems done today
2. Min-Stack Problem
Given a class MinStack, I have to design it to 
perform 4 operations in constant time complexity
    - push() 
    - pop()
    - top()
    - getMin() returns the min element in constant time

    * Approach One was to design the stack to hold pairs first element would the current element,
    and the second element would the minimum element encountered so far
    * Leetcode himself was not able to provide any more optimal approach
    * But people were telling me that it can be done using some mathematics(hashing)
    with a single element and single stack i.e. not storing pairs in the stack

3. Daily Temperatures
I maintained a monotonically decreasing stack here, since for a 
given value, I needed to get the next higher value after it
so by maintaining a monoto. decreasing stack I am storing all the
small values, and if I see a greater value after these values
I would be able to answer the question using the position of this
higher value.

**For now I am coding the listening to coldplay.** 





Since I am a programmer, I am doing coding and stuff for the majority of my life so 
it wouldn't be a surprise if my journal would contain stuff which I have learn in 
programming or some details of my work-life
Let me say this I have stopped caring about the work-life balance now
And my journal would be convoluted with diverse stuffs from this point on.
## 2025-03-31
#### Living the life in duality
I am going to live my life in duality and confusion, whatever things or thoughprocess I have
can be changed anytime
But I will always be a man of action, whatever happens I won't hestitate in taking action
I won't think about whether that action could a optimal action, good action or a action which will
harm me in future.


#### Studying of dev-container cli
I am going to do some practice with this tool for now
I tried unsuccessfully making the platform-dev container work, but it still is being a pain in the ass.

#### Restarting my interview preparation journey
- I am going to start solving the DSA problems once
- Will apply to 2 companies everyday
- The first topic which I am weak at and should focus on is recursion
- So I am going to solve CodeWithMik recursion (popular interview problems) playlist

## 2025-04-06
### Some understanding of the keus platform I've gained by deeper reading of the platform code
- that postman-remote-server.sh script starts after the we are able to successfully call the get the GetNodeConfig handler using moleculer gaterway
```js
checkNodeConfig() {
    NODE_CONFIG=$(curl --silent http://localhost:3000/keus/v1/node_configuration/GetNodeConfig)
    NODE_ID=$(jq -r '.nodeConfig.nodeId' <<< "$NODE_CONFIG")
    SITE_ID=$(jq -r '.nodeConfig.siteInfo.siteId' <<< "$NODE_CONFIG")

    echo $SITE_ID $NODE_ID $NODE_CONFIG
}
```
 This is the end

## 2025-05-30
1. My 160 rupees went down  the train, I ate some biryani from 2nd floor of dallas center 
   Biryani of there is very bad, and the chicken was too small to make it 160 rupees worthy
2. for lunch I am always gonna have the mess food, and then eat protein powder

## 2025-06-11

![[Pasted image 20250611234623.png|900]]

## 2025-07-31
It has been almost 2 months since I did any writing, I am just busy with this job at Keus, and also walking 8 kilometers everyday makes me very tired.

## 2025-10-27
Today after such a long time I am able to apply to a job opening
1. https://stripe.com/jobs/listing/software-engineering-new-grad/7176975/apply?gh_src=73vnei granted it was for freshers and I am working professional, but I just want to get out of my current company.
Some observations
I think the companies that are having 500-1000 people are the best and then a normal distribution follows


