#### Local Setup

- Install Scarb [Scarb Install](https://docs.swmansion.com/scarb/download)
- Run `scarb build`
- If VS Code User, just install a cairo 1 extension
- Replace `timepa` inside task.cairo to our project name `autostark`

### How It Works ?

Built for MVP. Very high level overview of how to create a task and execute it. There are others which are self-explanatory like cancel the job, get configs etc

#### Task Creation

For instance Alice wants to send xyz amount of eth to User1 and abc amount of eth to user2 after 20 days at some fixed time.

First Alice creates a task by calling a queue function where his intended calls are hashed and unique id is generated. His calls(in this case, transfer calls) total expenditure is calculated, assertion is made wether he holds the token to cover the expenditure or not. If he holds then we make a ERC20 approval to our contract(as spender). Now his id is stored. (only id not calls).

#### Task Execution

Task execution part is open to all, any one can call this function with exact set of calls of Alice. This approach sort of relax the part of relayers and necessity of maintaing network of bots. When execute function is called again id is generated from the supplied calls and checked against the id of Alice or other stored one's. If the id matches then time constrains are checked. Before execution of Alice calls ERC20 transferFrom is done to move the required assets from Alice to our contract as our contract would pay the fees and required token amounts. At last Alice calls would be executed and it's array of result would be returned.
