# Smart-Contract-Upgradeability
Proxy Upgradeability Considerations

Storage contract was build for future uses we don't know. We can store a lot of stuff

Both (proxy and functional contract) inherit from storage, and both contracts have this variables and structures from Storage
The difference is that we don't use mappings and variables from functional contract(Dogs). We only use variables inside
a proxy contract,
but functionality we use only from FUNCTIONAL contract(Dogs)

Then we upgrade Functional contract and added some new functions to contract(DogsUpdated)
Constructor and setting owner == msg sender doesn't work, because we didn't use delegatecall, and owner from proxy is equal 0;
So to do it in flexible way we add function initialize. And than we could make a delegatecall to that function in order to set
initial state in PROXY SCOPE. Otherwise it will fail, because in PROXY SCOPE before initialization owner is set to 0

In PROXY contract we have fallback function. Thats make possible to sort all functions that come to proxy delegate to FUNCTIONAL
CONTRACT.
In fallback function we use assembly code in order to delegate every function call.

It's VERY DANGEROUS to add state variables to FUNCTIONAL CONTRACT. It wil OVERWRIGHT, CORRUPT and RUIN other variables that 
is in proxy.



In real world environment we could inherit from olds contract in order just to build new functionality, but of course in the case 
if we have a BUG in old contract we need to overwright it in updated contract to fix it.


