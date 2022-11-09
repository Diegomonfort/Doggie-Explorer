<script>


export default {
  data() {
    return {
      owner: "",
      doggieName: "",
      description: "",
      imgUrl: "",
      listOfTraits:"",
      showhide:false,
      showshow: true,
      showhidealert: false,
      randomNumber: "",
      modelimg: ""
    }
  },




  methods: {
    async searchFunc() {

      // Here we want to known if the input value is over 10000 or lower than 0, if that is true, we recive a message of token id invalid.
      // The reason of this, is because there are only 10000 tokens
      if(document.getElementById('TOKENID_TXT').value >=10000 || document.getElementById('TOKENID_TXT').value < 0){
        document.getElementById('TOKENID_TXT').value= null;
        this.showhide = false;
        this.showshow = true;
        this.showhidealert = true;
      }
      // Here, if the user click on search and there is no text on input, it will hide the div
      if(document.getElementById('TOKENID_TXT').value == 0){
        this.showhide = false;
        this.showshow = true;
      }

      // Setting up the web3
      const Web3 = require("web3")
      const web3 = new Web3("https://cloudflare-eth.com")


      // ABI of the smart contract
      const ABI = [{"inputs":[{"internalType":"string","name":"baseURI","type":"string"},{"internalType":"string","name":"_name","type":"string"},{"internalType":"string","name":"_symbol","type":"string"},{"internalType":"address payable","name":"_sandOwner","type":"address"},{"internalType":"address","name":"_signAddress","type":"address"}],"stateMutability":"nonpayable","type":"constructor"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"owner","type":"address"},{"indexed":true,"internalType":"address","name":"approved","type":"address"},{"indexed":true,"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"Approval","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"owner","type":"address"},{"indexed":true,"internalType":"address","name":"operator","type":"address"},{"indexed":false,"internalType":"bool","name":"approved","type":"bool"}],"name":"ApprovalForAll","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"previousOwner","type":"address"},{"indexed":true,"internalType":"address","name":"newOwner","type":"address"}],"name":"OwnershipTransferred","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"bool","name":"_pause","type":"bool"}],"name":"TogglePaused","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"from","type":"address"},{"indexed":true,"internalType":"address","name":"to","type":"address"},{"indexed":true,"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"Transfer","type":"event"},{"inputs":[],"name":"allowedToExecuteMint","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"to","type":"address"},{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"approve","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"owner","type":"address"}],"name":"balanceOf","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"baseTokenURI","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"chain","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"_wallet","type":"address"},{"internalType":"uint256","name":"_amount","type":"uint256"}],"name":"checkMintAllowed","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"_wallet","type":"address"},{"internalType":"uint256","name":"_signatureId","type":"uint256"},{"internalType":"address","name":"_contractAddress","type":"address"},{"internalType":"uint256","name":"_chainId","type":"uint256"},{"internalType":"bytes","name":"_signature","type":"bytes"}],"name":"checkSignature","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"pure","type":"function"},{"inputs":[],"name":"contractAddress","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"erc1155Id","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"getApproved","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"indexWave","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"owner","type":"address"},{"internalType":"address","name":"operator","type":"address"}],"name":"isApprovedForAll","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"_wallet","type":"address"},{"internalType":"uint256","name":"_amount","type":"uint256"},{"internalType":"uint256","name":"_signatureId","type":"uint256"},{"internalType":"bytes","name":"_signature","type":"bytes"}],"name":"mint","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"name","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"owner","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"ownerOf","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"paused","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"_count","type":"uint256"}],"name":"price","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"renounceOwnership","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"from","type":"address"},{"internalType":"address","name":"to","type":"address"},{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"safeTransferFrom","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"from","type":"address"},{"internalType":"address","name":"to","type":"address"},{"internalType":"uint256","name":"tokenId","type":"uint256"},{"internalType":"bytes","name":"_data","type":"bytes"}],"name":"safeTransferFrom","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"_address","type":"address"}],"name":"setAllowedExecuteMint","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"operator","type":"address"},{"internalType":"bool","name":"approved","type":"bool"}],"name":"setApprovalForAll","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"string","name":"baseURI","type":"string"}],"name":"setBaseURI","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"_owner","type":"address"}],"name":"setSandOwnerAddress","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"_signAddress","type":"address"}],"name":"setSignAddress","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"_waveType","type":"uint256"},{"internalType":"uint256","name":"_waveMaxTokens","type":"uint256"},{"internalType":"uint256","name":"_waveMaxTokensToBuy","type":"uint256"},{"internalType":"uint256","name":"_waveSingleTokenPrice","type":"uint256"},{"internalType":"address","name":"_contractAddress","type":"address"},{"internalType":"uint256","name":"_erc1155Id","type":"uint256"}],"name":"setupWave","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"signAddress","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"bytes4","name":"interfaceId","type":"bytes4"}],"name":"supportsInterface","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"symbol","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"toggleSale","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"index","type":"uint256"}],"name":"tokenByIndex","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"owner","type":"address"},{"internalType":"uint256","name":"index","type":"uint256"}],"name":"tokenOfOwnerByIndex","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"tokenURI","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"totalSupply","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"from","type":"address"},{"internalType":"address","name":"to","type":"address"},{"internalType":"uint256","name":"tokenId","type":"uint256"}],"name":"transferFrom","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"newOwner","type":"address"}],"name":"transferOwnership","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"waveMaxTokens","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"waveMaxTokensToBuy","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"waveSingleTokenPrice","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"waveTotalMinted","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"waveType","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"}];
      
      // Adress of smart contract
      const ADDRESS = "0xC7dF86762ba83f2a6197e1Ff9Bb40ae0f696B9E6"

      //Setting up the contract with the adress and ABI
      const contract = new web3.eth.Contract(ABI, ADDRESS);

      // Making the fetch of the smart contract
      const urlJSON = await contract.methods.tokenURI(document.getElementById('TOKENID_TXT').value).call();
      const owner = await contract.methods.ownerOf(document.getElementById('TOKENID_TXT').value).call();
      const response = await fetch(urlJSON);
      const dataJson = await response.json();

      // Here we are takin the methods of the ABI and giving them a variable
      this.owner = owner;
      this.doggieName = dataJson["name"];
      this.imgUrl = dataJson["image_url"];
      this.modelimg = dataJson["external_url"];
      this.description = dataJson["description"];
      this.listOfTraits = dataJson["attributes"];
    
      this.showhide = true;
      this.showshow = false;
      this.showhidealert = false;

      // Console logs to help me
      console.log("a", contract);
      console.log("Url owner:",owner);
      console.log("Url name:",dataJson["name"]);
      console.log("Url image_url:",dataJson["image_url"]);
      console.log(dataJson["external_url"]);
      console.log("Url description:",dataJson["description"]);
      console.log("Url (List of traits) attributes:",dataJson["attributes"]);
    },
    
    // Function to close error alert
    closealert(){
      this.showhidealert = false;
    },

    // Random Function
    randomnum () {		
     this.randomNumber = Math.floor(Math.random() * 10000);
     console.log(this.randomNumber);
     document.getElementById('TOKENID_TXT').value = this.randomNumber;
     this.searchFunc();

    } 
  }

  
}
</script>

<template>
  
  <!-- In the "container" div we have the doggie explorer logo, the input field, the search and random buttons -->

  <div class="container">
    <img class="imglogo" src="https://diegomonfort.com/muestras/doggies/doggies-web4.png" alt="">
    <br>
    <br>
    <input class="inputcls" placeholder="Token Id" type="number" id="TOKENID_TXT">
    <div v-if="showhidealert" class="alertbox">
      <p>Invalid Token ID</p>
      <a class="close" @click="closealert">&times;</a>
    </div>
    <button class="buttoncls" @click="searchFunc">Search<i class="fa fa-search"></i></button>
    <button class="buttoncls" @click="randomnum">Random<i class="fa fa-random"></i></button>
  </div>
  
  <!-- In the "container2" div we have the card with all the information of the doggie, included the 3d model -->

  <div class="container2" v-if="showhide" >
    <div class="row1">
      <p class="doggienamecls" v-if="showhide">{{ doggieName }}</p>
      <a v-bind:href="modelimg" target="_blank"><img class="imgcls" :src="imgUrl" width="312" height="312" v-if="showhide"></a>
      <a v-bind:href="modelimg" target="_blank"><button @click="modelimg" class="buttoncls3d"><i class="fa fa-cube"></i> 3D view</button></a>
      <p class="ownercls" v-if="showhide">{{ owner }}</p>
      <p class="descrcls" v-if="showhide">{{ description }}</p>
      <table v-if="showhide" id="traitstable">
            <thead>
                <tr>
                    <th>Trait</th>
                    <th>Value</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="traits in listOfTraits" :key="traits">
                    <td>{{traits.trait_type}}</td>
                    <td>{{traits.value}}</td>
                </tr>
            </tbody>
        </table>
      </div>
      
  </div>

  <!-- Simple Footer -->
  <footer>
        <a href="https://www.sandbox.game/en/" target="blank"><img  class="footerlogo" src="https://www.sandbox.game/img/01_Top_Bar/TSBLogo-mobile.svg" alt=""></a>
  </footer>
</template>

<style>

/* And finally we have the style of the page */


/* This code help us to hide the arrows in the input field */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}


.container{
  background-color: transparent;
  color: black;
  text-align: center;
  font-family: 'Montserrat', light;
  font-weight: 500;
}
.tokenidtext{
  color: black;
  font-weight: 500;
}

.imglogo{
  width: 210px;
}

.footerlogo{
  width: 150px;
}

.inputcls{
  background: transparent;
  outline: none;
  border: 1.5px solid #ffffff;
  height: 30px;
  min-width: 215px;
  text-align: center;
  font-size:14px;
  font-family: Montserrat, sans-serif;
  font-weight: 500;
  border-radius: 5px;
  color: #fff;
}
::placeholder {
  color: white;
}
.alertbox{
  max-width: 220px;
  margin:20px auto;
  padding:1px;
  position:relative;
  background-color: #a0222f;
  color: white;
  border-radius: 5px;
}

.close{
  position:absolute;
  color: #ffffff;
  width:10px;
  height:10px;
  opacity:0.5;
  right:15px;
  top:1px;
  text-align:center;
  font-size:1.6em;
  cursor:pointer;

}

.buttoncls{
   background-color: #E67B00;
   border-radius: 5px;
  border: none;
  color: #fff;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: block;
  font-size: 14px;
  margin: 20px auto;
  cursor: pointer;
  font-family: Montserrat, sans-serif;
  font-weight: 500;
  min-width: 220px;
}

.buttoncls3d{
   background-color: #025175;
   border-radius: 5px;
  border: none;
  color: #fff;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: block;
  font-size: 12px;
  margin: 20px auto;
  cursor: pointer;
  font-family: Montserrat, sans-serif;
  font-weight: 500;
  min-width: 100px;
}
a:link {
  text-decoration: none;
}

.container .fa-search{
  position: relative;
  left: 65px;
}
.container .fa-random{
  position: relative;
  left: 60px;
}


.container2{
  background-color: rgba(0, 161, 230, 0.562);
  color: black;
  width: 40%;
  height: 560px;
  margin: 0 auto;
  margin-top: 50px;
  padding: 10px 60px;
  padding-bottom: 65px;
  text-align: center;
  overflow: auto;
  box-sizing:border-box;
  border-radius: 10px;
}


.row1{
  float: center;
}

.doggienamecls{
  font-weight: 500;
  text-align: center;
  font-size: 20px;
  text-transform: uppercase;
    letter-spacing:7px;
    color: #fff;
}

.ownercls{
  color: #fff;
  font-weight: 200;
  text-align: center;
  font-size: 12px;
  }

.descrcls{
  color: black;
  font-weight: 300;
  font-size: 12px;
  text-align: center;
}

.imgcls{
  height: 380px;
  width: 380px;
  border-radius: 18px;
}

#traitstable {
  font-family: 'Montserrat', light;
  border-collapse: collapse;
  width: 100%;
  margin-top: 30px;
}

#traitstable td, #traitstable th {
  border: 2px solid transparent;
  padding: 8px;
  font-size: 12px;
  text-align: left;
  margin: 2px;
  padding-left: 20px;
}

#traitstable tr:nth-child(even){background-color: #c4c4c4; color: rgb(0, 0, 0);}
#traitstable tr:nth-child(even):hover {background-color: #c5c5c5}

#traitstable tr:hover {background-color: #E67B00;}

#traitstable th {
  padding-top: 6px;
  font-size: 12px;
  padding: 10px;
  padding-left: 20px;
  text-align: left;
  background-color: #025175;
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.4);
}



.logocls{
  width: 100%;
  position: relative;
  margin-top: 90px;
}

/* This 3 styles are for the scrollbar */

/* width */
::-webkit-scrollbar {
  width: 3px;
  
}
/* Track */
::-webkit-scrollbar-track {
  background: transparent; 
}
/* Handle */
::-webkit-scrollbar-thumb {
  background: #c0c0c0; 
  border-radius: 20px;
}

footer{
  margin-top: 60px;
  text-align: center;
}

@media (max-width: 730px){
  .container2{
    background-color: rgb(255, 255, 255,  0.4);
  color: black;
  width: 290px;
  height: 600px;
  margin: 0 auto;
  margin-top: 50px;
  padding: 10px;
  padding-bottom: 40px;
  text-align: center;
  overflow: auto;
  box-sizing:border-box;
  border-radius: 10px;
}
.imgcls{
   height: 190px;
  width: 190px;
  border-radius: 14px;
}

.buttoncls3d{
   background-color: #025175;
   border-radius: 5px;
  border: none;
  color: #fff;
  padding: 7px;
  text-align: center;
  text-decoration: none;
  display: block;
  font-size: 10px;
  margin: 10px auto;
  cursor: pointer;
  font-family: Montserrat, sans-serif;
  font-weight: 500;
  min-width: 50px;
}

.doggienamecls{
  font-size: 15px;
}

.ownercls{
  font-size: 9px;
  }

.descrcls{
  color: black;
  font-weight: 300;
  font-size: 10px;
  text-align: center;
}


#traitstable td, #traitstable th {
  border: 2px solid transparent;
  padding: 8px;
  font-size: 10px;
  text-align: left;
  margin: 2px;
  padding-left: 20px;
}

#traitstable tr:nth-child(even){background-color: #c4c4c4; color: rgb(0, 0, 0);}
#traitstable tr:nth-child(even):hover {background-color: #c5c5c5}

#traitstable tr:hover {background-color: #e5e2e2;}

#traitstable th {
  padding-top: 6px;
  font-size: 12px;
  padding: 7px;
  padding-left: 20px;
  text-align: left;
  background-color: #025175;
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.4);
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: transparent; 
  border-radius: 20px;
}

}

</style>