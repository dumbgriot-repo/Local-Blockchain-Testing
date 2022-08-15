# Local-Blockchain-Testing
Learnweb3 tutorial for local smart contract testing

Local Blockchain Testing
This tutorial should familiarize you with starting a local blockchain using Hardhat, deploying a sample smart contract to the local blockchain and interacting with that blockchain with Metamask and Remix.

Why local blockchain?
It is very useful to run a local blockchain because testing becomes very fast and efficient.
Its only your machine which is running the blockchain and thus consensus is fast and you dont have to wait for other nodes to sync or validate.
You can also use many specialized modules specially built for local testing like Hardhat console.log which helps you to add printing inside your contract.
🤔 Why is testing on local blockchain faster?


Because only your computer is running the node so consensus happens faster

Because the code is more efficient when run locally
Build
To build the smart contract we would be using Hardhat. Hardhat is an Ethereum development environment and framework designed for full stack development in Solidity. In simple words you can write your smart contract, deploy them, run tests, and debug your code.

To setup a Hardhat project, Open up a terminal and execute these commands

npm init --yes
npm install --save-dev hardhat
In the same directory where you installed Hardhat run:

npx hardhat
Select Create a basic sample project
Press enter for the already specified Hardhat Project root
Press enter for the question on if you want to add a .gitignore
Press enter for Do you want to install this sample project's dependencies with npm (@nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers ethers)?
Now you have a hardhat project ready to go!

If you are not on mac, please do this extra step and install these libraries as well :)

npm install --save-dev @nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers ethers
and press enter for all the questions.

The basic hardhat project also comes with a sample smart contract. We'll be using this smart contract in our example. You should see this contract in contracts\Greeter.sol. It should look something like this:

//SPDX-License-Identifier: Unlicense
pragma solidity ^0.8.0;

import "hardhat/console.sol";

contract Greeter {
    string private greeting;

    constructor(string memory _greeting) {
        console.log("Deploying a Greeter with greeting:", _greeting);
        greeting = _greeting;
    }

    function greet() public view returns (string memory) {
        return greeting;
    }

    function setGreeting(string memory _greeting) public {
        console.log("Changing greeting from '%s' to '%s'", greeting, _greeting);
        greeting = _greeting;
    }
}
This contract declares a string - greeting. There are also two methods and a constructor. The constructor initiates the greeting variable with the provided string value.
The greet method returns the greeting string. Since this is a view function, it costs no gas, and requires no signing to execute.
The setGreeting method sets the greeting string with a provided user value. Since this updates the smart contract state, it costs gas, and requires signing. One interesting thing to note about the setGreeting method is that it uses the Hardhat's console.log contract, so we can actually debug and see to what values was greeting changed to!
🤔 Which contract did we use for debugging?


hardhat/debug.sol

hardhat/debugging.sol

hardhat/console.sol
Now to actually start running your local blockchain in your terminal pointing to your directory execute this command:

npx hardhat node
(Keep this terminal running)

This command starts a local blockchain node for you. You should be able to see some accounts which have already been funded by hardhat with 10000 ETH

🤔 Which command did you use to start your local blockchain?


npx hardhat local start

npx hardhat node

npx hardhat local chain
Image

Now, you can continue by deploying the contract to the local blockchain using Hardhat, by running npx hardhat run scripts/sample-script.js.

Alternatively, you can also use something like Remix and have it deploy contracts to your local blockchain. The second method will also involve setting up Metamask to work with your local blockchain, and will give you an idea of how to locally test your React/Next.js apps using contracts running on the local blockchain as well, so let's do that.

Metamask Connection
To use metamask to connect to this network, click on your profile and then click on settingsImage

Then click on Networks, followed by Localhost 8545Image

Image

Change the Chain ID to 31337(this is the chainId for the local blockchain you are running) and then click SaveImage

Awesome now your MetaMask has a connection to your local blockchain, we will now add the accounts that Hardhat gave to us

In the node terminal, you should see several accounts displayed. Let's grab one of those:

Account #0: 0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 (10000 ETH)
Private Key: 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80
Go to metamask --> click on your profile --> import account. Select private key in the dropdown and paste the private key from the account you wish. You should now see an account with 10000 ETH

🤔 What is the chain id for a local hardhat node?


1337

31337

3133

42069
Remix
We will now deploy our contract to local blockchain and interact with it using Remix

Go to remix.ethereum.org and create a new file inside the contracts folder named Greeter.sol

Copy this code into it:
//SPDX-License-Identifier: Unlicense
pragma solidity ^0.8.0;

import "hardhat/console.sol";

contract Greeter {
    string private greeting;

    constructor(string memory _greeting) {
        console.log("Deploying a Greeter with greeting:", _greeting);
        greeting = _greeting;
    }

    function greet() public view returns (string memory) {
        return greeting;
    }

    function setGreeting(string memory _greeting) public {
        console.log("Changing greeting from '%s' to '%s'", greeting, _greeting);
        greeting = _greeting;
    }
}
This is the same code, we explained above

Compile Greeter.solImage

Now to deploy, go to deployment tab and in your environment select Injected Web3, make sure that the account connected is the one that you imported above and the network is Localhost 8545 on your MetaMask

ImageImage

Set a greeting and click on deploy

Your contract is now deployed 🎉

Set a greeting and click on setGreeting

Image

Check your terminal which was running your hardhat node, it should have the console.log

Image

🤔 Can MetaMask and Remix connect with your local blockchain?


Yes

No
Contributors
This module was built in collaboration with Hypotenuse Labs

🤔 Can you trust a dApp running on someone's local node?


Yes

No
🤔 Can you use Hardhat's console.sol library on regular Ethereum networks? Select the best option


No it only works with the local node

Yes we can use it anywhere

No it will give a compilation error

Yes but it is much harder to read those logs
Submit Quiz
