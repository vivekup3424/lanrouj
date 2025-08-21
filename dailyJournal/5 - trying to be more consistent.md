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
