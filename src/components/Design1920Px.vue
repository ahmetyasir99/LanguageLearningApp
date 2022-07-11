<template>
  <div class="background">
    <div class="logoDiv">
      <img
        class="logo"
        src="https://weborigo.com/assets/img/logos/weborigo-logo-orange-white.svg"
      />
    </div>
    <div class="content">
      <!-- <img style="  position: absolute;
  
    display: block;
    object-fit: contain;
    margin: 0 auto;
    height: 50%;
    width: 100%;
    filter: drop-shadow(-6px 6px 10px rgba(255, 103, 0, 0.12));
    border-radius: 10px; z-index: 0; margin: 0 auto;" src="https://www.wappoint.co.za/wp-content/uploads/elements/template-6-1566392822/shape-gradient.png" alt=""> -->
      <div class="ratesTop">
        <div style="display: flex">
          <v-icon style="margin-right: 5px; color: #ff6700">
            mdi-thumb-up-outline
          </v-icon>
          <div class="rates" v-text="trueRate"></div>
        </div>
        <div style="display: flex">
          <v-icon style="margin-right: 5px; color: #ff6700">
            mdi-thumb-down-outline
          </v-icon>
          <div class="rates" v-text="falseRate"></div>
        </div>
      </div>
      <div class="imageDiv">
        <img class="picture" :src="currentImage" />
      </div>
      <div  class="restDiv">
        <div v-text="currentWord" class="word"></div>
        <input
          @keyup.enter="wordSelector"
          v-model="inputWord"
          class="input"
          type="text"
        />
        <button
          :disabled="!inputWord || isDisabled"
          @click="wordSelector"
          class="result"
        >
          Let's see
        </button>
        <div class="ratesBottom">
          <div style="display: flex">
            <v-icon style="margin-right: 5px; color: #ff6700">
              mdi-thumb-up-outline
            </v-icon>
            <div class="rates" v-text="trueRate"></div>
          </div>
          <div style="display: flex">
            <v-icon style="margin-right: 5px; color: #ff6700">
              mdi-thumb-down-outline
            </v-icon>
            <div class="rates" v-text="falseRate"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      wordList: [
        {
          serbian: "srećan",
          english: "happy",
          picture:
            "https://s3-alpha-sig.figma.com/img/2983/484c/02f1f51da2aaae1b0f190e4b632adfa8?Expires=1658707200&Signature=DUy2vHeEYCmnIuQf5u8mGSYQMBhOLyJo-w0IojlwdbZCdiFb~R-i0TKnH1MTl89L7CSgvD3L2Tu-VZa-6Sle8tcheZf66hURpyxlC8WKBC0ltxnwAHBJljEeOX4E~1knZdxEW3eTjhu3fw8ssDZ24jhcrpGmAFVa2YAAwExu9KXiyMNTIi2hAzpC3tZ4BmOTg1u7If5WnXdfMCzvCuuaMt5IyNlFCBiuhj8SRm1ERRySd1FWQjuO93je0Q22j0nii4z7gu~AYWlPn8SMNnwlRf2lOLIKq6QdHF-2-D0WoaVYLvIF6Mb05PAwF~Zz7krISuz5HVM2JxjNcDNsoUJkaw__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
        {
          serbian: "lijepo",
          english: "nice",
          picture:
            "https://s3-alpha-sig.figma.com/img/63bc/75b3/8447a61b88ed25bd53aa7c14faeb3d2e?Expires=1658707200&Signature=OiWzwqn0WAmDV32iijzEq~u-J6dQTFmr0rVUNfvhnOjbYDG5UOfXcbjocNIcwS31htPr2LpQIAj18Ea-GwsWP3j4fyoaYkpeL2sGg80AIN8j27k5X97o6feZ15zq0EhlXe6j3ENfGphQjlyuBi4SRyOGyKcva2KxJx4JPv3RuQO4mFhZp4GtpCGTws9Og171XQYwEL6yUZ0tMsGncchHCWXGt9PFPHeHCUhJDkhRZgBfRsIcyFzcLFMKdbaL8vR3C0PDH7M3TrAG3K2oDF9LahZd4vxk0AVWLjVHWfeeIIOSdpLw9YaI00j1wRkFbnzkOgUb6zVMIGPSS3l~W~cMkg__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
        {
          serbian: "prijatelju",
          english: "friend",
          picture:
            "https://s3-alpha-sig.figma.com/img/df74/0864/b039d5e3bc983722eb3c24062883dba7?Expires=1658707200&Signature=NSSD50aL9fhRfkO6kXV4kfoncnjTkWBn5XOX~qdT8M9Lezy~sBLBbHSvh9W2G42R40W6lyxK-cHxLt~~8AB~RBMBgrSFO-vgBToEi~3i-gXSnjpklE4HaEtbImZrtv7wJ56qm0pEz8i6QJ9NCvwoRzhQCKSz77Js0smxEcxcbb-cTxEjYmK1zhvGEQSlR3jQ0K-AaNKABXiBfg1WOWOydqQCRpEkCkNNq4nMLu0fmCBfdmiTHUt9bLKmIqpE6iAkH48M2J-pjD2GRs6xbFalygUXmc02RdoXP-RIioUaiezc-HUnhuEgkDWgsn0vlRP0yFyjhTXc6M0xz2k0sGnxhQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
        {
          serbian: "eksplozija",
          english: "explosion",
          picture:
            "https://s3-alpha-sig.figma.com/img/25cb/0b30/9e70d171faf4dd65df375f6965a014e8?Expires=1658707200&Signature=QJr7JqFyOinqh6B-zFbl-9uVMUP6wuttV9-6JQvVVOGfysUCNVnb4wF8V5Mi856wenPEDZIbLDJSpn~2nPJKoABol983bLKenGVW0qWPCO1Xgt~HFUVxyQygxmD3-wm0fwCbLxRdzXBdiGrYOJLxOmPPKOV3FzS4L2nUXLTbawAKqkMOEcAhN2M8MavP8nPsu~WkOjy0SKcwv70un7xuoBfTABy-yDZTxifiqa-0wgvhb9-C5cDXMe7Yg~ZidNR3D~872zrXSpnc3a1GndK0yXRb0xunrzKrRTBwLx725JpA27hbIes2bh1~sHHOpKStU0FYfDxXu55p8Zz9UK-CgA__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
        {
          serbian: "šargarepa",
          english: "carrot",
          picture:
            "https://s3-alpha-sig.figma.com/img/c09f/748d/268d99ea6c0977fbecd771db9f691c3e?Expires=1658707200&Signature=TYisnqiOEhm0GnFLoSHsyXbpQDGRVVZvRpq0DsQLrUM5j~c1tExQXExxKbKEsOCC~TzLXR54SweS6hi9zPSMA5rQhjZ2Tf8qxV-Nf6k52xTykMgvIG~cbhLvscyj42ftiTT0yQA-mN5r~2Pe4Q8wmuKDiHTxAWjkB-3CfOvRT7Pa2imwkejhduS6UNQtrX29KY5enSVCVrLVFvhKMpdc1KxP1maD0nQJLQLDqUSLnzwJIjVgeqUkcjYtwzefj7K0JNrlUUP0I7VU99QsnODQjcfQUOM2hkIlDGb0TYW~dpzv8IKHZaF3fcOLEcfcCXJGkZh7de3788g6I7hOivTDfA__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
        {
          serbian: "auto",
          english: "car",
          picture:
            "https://s3-alpha-sig.figma.com/img/8e18/9198/b596ec8aaf473f1bb3851e23f55a92f0?Expires=1658707200&Signature=U0G9lk3ckeEDWdHtCexPVqeSm-1DgTyECznmxvMtN5BBZvwgqUYRDchT8XjmYq8H6I3O6nEfx~rzw7o4~QcZfbZdwoErwNWpbXwT-m673zk55SXnqoVMAJcol5Ash3vninGDmwAjIBu9tNQFM6ZMvhOsSsxLmhtkNu7vz2ekcqkyCN23b4ym3~Yy6W6Hli7JGX0p77uf6drDsJkZyZe2sXlnarJzlGId-ddgnnfiT6nyl99uuWDcHNq5yEm2rLQnj9d-sHU7LOWSct5u1wGsc2QHZgrviylk0CXt6lrA6TLHryi2X0ylmVnclQQLYR6Dmzwl6ub9TlXvGetLqM~eYQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
        {
          serbian: "vojnik",
          english: "soldier",
          picture:
            "https://s3-alpha-sig.figma.com/img/e6c4/e378/dda598c32858068ec7cebc8c26f9df6c?Expires=1658707200&Signature=TV3wuC~ZSE867CJ1HJYW7lkPYLtaLPjhE2ABjzs9aHb41bPmt9XxinVVv62wwsDs8hJlJ2Oxidis4tLLwIS6XQ9RVwEFpL-PfU9g3WSHaDaTpndhuBdLvSGaKSOPK8z9XdDxVmzewKczpn7~NV6ak1Jye6iTgsVZ8Ja8CYN20YDn0P-swAXAjW5mUSHlfHol1hKTfr~UfvbZioDnSa7Hrl3b-0Q5IeYLV~sTgUqAXazVYF1ipZ32h6AgvPJuGBfRbA3-ungcj1BcH4fGKW2ybCH1zuGNTtBHnfXehNq7Gd5mNI~JtbbLRyFY5xGcdMrJ03aqBI7JcRk~iq5cEtOYxg__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
        {
          serbian: "strah",
          english: "fear",
          picture:
            "https://s3-alpha-sig.figma.com/img/423f/b29d/f9abc1016fe45822c7a14f624eafd6c2?Expires=1658707200&Signature=BgPsrj1A5NG7sswZsxmjNw7i3dyKd1RJiLFFZdjicRZ6f~dtWcThDwmDh1dojqxC007rSpxjU-4HPiEZPCCPXapoL47qGIr8aYSldm3gMDSblB1e2adDlBRCsuraR7dpkhP6DZKSJOZc6RAsd54rYa27E0gx6dGwUTCugP9kXirkAZylcc67IopZYjVtuRFa97OobnfG~ZW3Fv1M5MU5Cz7ZfpNFD3Aj6TJR7stEL7rOBk9RBxMgz-Rk-c3jgf2hKu6maIz3AfKp9KJpPEs-7UMgJyT9GhwW47o~OrU~SpMIb2KNByU90Au84xtQledpodnrx-NVPlBl2iVDjZjFEQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
        {
          serbian: "relativnost",
          english: "relativity",
          picture:
            "https://s3-alpha-sig.figma.com/img/a617/2683/e30b1f7879b08f994fbcda8a22d172f4?Expires=1658707200&Signature=JYlNypK8odUeVHRqKHtZqCk5efBXo83syiTk2gZOMfjlLh-RZVG0qNwH2b5GbGJ1ichUbbcDS9GVjPuisjhZudodOSroGvBpuMndvI3mwvrl735oQa63YyYbyZiZKuZN4~PGrFAOxemSJCRhQTdphsNyaHqF5UAtJahertNyy6aY2tO3PFiTDsdmT34osQHkgWFNKbgcVhEXE537-QBNouXPJ~UDiGPvjhyi2-lOLcdKQqHf60yw4iajNatz8Z~XwyvTqmmV1tQmU4tTvFBvjlyorh4MklhLV~CMdinF-hbuHD9mCqaoqQG0IeEnfgNByw~JfJQrbVT1fd7aNvDHkA__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
        {
          serbian: "knjiga",
          english: "book",
          picture:
            "https://s3-alpha-sig.figma.com/img/635e/24c0/f44761170f05f7b8cec0c164ffe3f7ab?Expires=1658707200&Signature=N4SmOzhXvXV7glOaAl~e~hJjjyk7WDOMjKW8m4LKQwdp7hbjem5JwfxuZs0G95T2VofbGylGJ3yU979XgYL3mD~wi2m~GYe1~Egi1cZg~PWYrXpSjD~V5UQYEUGjM8VEBZjI3Tok5NJ2aSjQrQ8nZ8x8DGB2LXG6anMGNgIJFFCCMzLRpbk5OKAaGxv~eB8jsyNal7AXwaAmRY7f5VSWfWqd04qkdxpKryxJcjSfKdXyZ-SjZVLe5hPcITgclBZFR1QzzXAU3MnzoZqH53DJQ6ZifUZ8OY1o7b27Bn-XBSOsGUM53nTf1WcEDLR1bYXaAJHg2u5meg1f3JkZfp73FA__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
        {
          serbian: "Zemlja",
          english: "Earth",
          picture:
            "https://s3-alpha-sig.figma.com/img/9b88/f050/d77f5b07ac36cc4e4d17fb5f31806f2c?Expires=1658707200&Signature=ZBy56zocZcI5nWelqgLfyzrRkr7nIZaFxYNNz77c-YGcTfNqidXFEfunBWp0CHjG95HbBRjgH~CN18FXVOBwRxheP4kArjqhZCN-945XOH3ggxBGgSMv7Mv0scYlqdlT1yIQK6gwU7DZDxWa7FnIYIqiSL3YsQ58blhThJo-3DTXfP6s0VS3mTGOY-qiNyzbTFB7bai8olUnTFiEP4lxFKd07Ybc2f59lTSOGRc670PMskyDl3JeY5jBPnxECqiQ1TVnrO-3orf8shMPpswk3VQ5D8-3zxHIGm1lksk8OX9ntb3bBgS6WtdHaYm8Pgu6ifKqDTpyZp5IVl4NB5I5MQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
        {
          serbian: "ograničenje brzine",
          english: "speed limit",
          picture:
            "https://s3-alpha-sig.figma.com/img/abad/8b66/af5c7ba0826d7cceb5d5b6782349fa7c?Expires=1658707200&Signature=furk8wHX-TDWK1j2s9ReRi79LZLWjPepmwXzooHjS3BGTaf5NogVURbQryB76A2q03tqhFhtu6pGBC4TNv2OB2iKUmj16isXCaAu4UqZfHE~hLw~VNr1eWBiRAM29IGVGxAMuzeFsIfqxi7cr3QfNHq1gGVn3NtGlnzu9TmBknbgQ0hJoWHACEiZ3WsA-VwQorisdzt823KNWZ43jqhRhbDWAd6QDChYU7Fp9DJdpoeDcnd0h-AjdJa0U-S8xipev9qLOKjDCZhg7sKxoGc-4XDTnDeiPglzBMb1lNpD-rdLEPEFV-CsdO8QQAW7CW8m5g6P9oct3SS6ow5zGDQm7Q__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        },
      ],
      inputWord: "",
      currentWord: "",
      answerWord: "",
      wordIndex: 0,
      numberOfTrue: 0,
      numberOfFalse: 0,
      trueRate: "0 / 0",
      falseRate: " 0 / 0",
      totalAttempts: 0,
      isDisabled: false,
      currentImage: "",
    };
  },
  mounted() {
    this.wordSelector();
    this.initialWordNumber = this.wordList.length;
    console.log(this.initialWordNumber);
  },
  methods: {
    wordSelector() {
      if (this.wordList[0]) {
        if (this.currentWord) {
          this.result();
        }
        this.wordIndex = Math.floor(Math.random() * this.wordList.length);
        this.currentImage = this.wordList[this.wordIndex].picture;
        console.log(document.getElementsByClassName("picture").src);
        let randomLanguage = Math.round(Math.random());
        const language = randomLanguage == 0 ? "serbian" : "english"; //random oalrak dil belirleme
        const ansLanguage = language == "serbian" ? "english" : "serbian"; //belirlenen dilin zıttı, cevap için
        this.currentWord = this.wordList[this.wordIndex][language]; //ekranda görülecek dildeki kelime
        this.answerWord = this.wordList[this.wordIndex][ansLanguage]; //yazılması gereken dildeki karşılığı

        console.log("wordIndex:", this.wordIndex);
        console.log("currentword:", this.currentWord);
        console.log("answer:", this.answerWord);
        console.log(this.wordList);
        this.inputWord = "";
      } else {
        this.isDisabled = true;
        this.currentWord = "Congratulations";
      }
    },
    result() {
      this.totalAttempts += 1;
      if (this.inputWord == this.answerWord) {
        this.wordList.splice(this.wordIndex, 1);
        this.numberOfTrue += 1;
        this.trueRate = this.numberOfTrue + " / " + this.totalAttempts;
        this.falseRate = this.numberOfFalse + " / " + this.totalAttempts;
      } else {
        this.numberOfFalse += 1;
        this.trueRate = this.numberOfTrue + " / " + this.totalAttempts;
        this.falseRate = this.numberOfFalse + " / " + this.totalAttempts;
        //yeni bir kelime göster
        console.log("hey");
      }
    },

    languageSelector() {
      this.language = Math.round(Math.random());
    },
  },
};
</script>

<style scoped>

  .background {
    background-repeat: repeat;
    height: 100%;
    background: #ff6700;
    display: flex;
    flex-direction: column;
    justify-content: start;
  }
  .logoDiv {
    margin-top: 10px;
    display: flex;
    flex-direction: column;
    max-height: 100px;
   
  }
  .logo {
   
    margin: 0 auto;
   
    height: 80%;
    margin-top: 5px;

    
  }
  .content {
    margin: 0 auto;
    width: 80%;
    
    display: flex;
    flex-direction: column;
   
    justify-content: start;
    background-color: white;
    margin-bottom: 10px;
    box-shadow: 0px 8px 16px rgba(0, 0, 0, 0.16);
border-radius: 10px;
  }
  .imageDiv {
    
    width: 100%;
    display: flex;
    flex-direction: column;
  }

  .picture {
    position: relative;
    z-index: 2;
    display: block;
    object-fit: contain;
    margin: auto;
    height: 100%;
    max-height: 100%;
    width: 80%;
    filter: drop-shadow(-6px 6px 10px rgba(255, 103, 0, 0.12));
    border-radius: 10px;
    margin-top: 15px;
  }
  .restDiv {
   min-height: 200px;
   max-height: 80%;
    z-index: 2;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
  }
  .word {
    z-index: 2;
    font-family: "Roboto";
    font-style: normal;
    font-weight: 600;
    font-size: 24px;
    line-height: 28px;
    color: #222222;
    margin: 0 auto;
  }
  .input {
    background: #ffffff;
    box-shadow: -6px 6px 10px rgba(255, 103, 0, 0.3),
      6px -6px 10px rgba(231, 190, 163, 0.3);
    border-radius: 10px;
    margin: 0 auto;
    width: 50%;
    min-height: 40px;
  }
  .result {
    background: #ff6700;
    border-radius: 10px;
    width: 250px;
    height: 60px;
    margin: 0 auto;
    font-family: "Roboto";
    font-style: normal;
    font-weight: 900;
    font-size: 24px;
    line-height: 28px;
    color: #ffffff;
  }
  .rates {
    color: #ff6700;
    font-family: "Roboto";
    font-style: normal;
    font-weight: 300;
    font-size: 20px;
    line-height: 23px;
  }
  .ratesBottom {
    display: flex;
    margin: 0 auto;
    width: 100%;
    justify-content: space-around;
  }
  .ratesTop {
    display: none;
  }


@media screen and (max-width: 1280px) {
     .background {
        height: 100vh;
    }
  .word {
    z-index: 2;
    font-family: "Roboto";
    font-style: normal;
    font-weight: 600;
    font-size: 20px;
    line-height: 23px;
    color: #222222;
    margin: 0 auto;
  }
  .input {
    min-height: 36px;
  }
  .result {
    height: 50px;
    font-size: 20px;
    line-height: 23px;
    color: #ffffff;
  }
}

@media screen and (max-width: 380px) {
    .background {
        height: 100vh;
    }

  .logoDiv {
    display: flex;
    flex-direction: column;
   
    
  }
  .logo {
    margin: 0 auto;
   
    max-height: 200px;
    
    
  }
  .content {
    margin: 0 auto;
    width: 80%;
    display: flex;
    flex-direction: column;
    

    background: #ffffff;
    margin-bottom: 10px;
    box-shadow: 0px 8px 16px rgba(0, 0, 0, 0.16);
    border-radius: 40px;
  }
  .imageDiv {
    
    width: 100%;
    display: flex;
    flex-direction: column;
  }

  .picture {
    position: relative;
    z-index: 2;
    display: block;
    object-fit: contain;
    margin: auto;
    height: 100%;
    max-height: 95%;
    width: 80%;
    filter: drop-shadow(-6px 6px 10px rgba(255, 103, 0, 0.12));
    border-radius: 10px;
  }
  .restDiv {
    z-index: 2;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
  }
  .word {
    z-index: 2;
    font-family: "Roboto";
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 19px;
    color: #222222;
    margin: 0 auto;
  }
  .input {
    background: #ffffff;
    box-shadow: -6px 6px 10px rgba(255, 103, 0, 0.3),
      6px -6px 10px rgba(231, 190, 163, 0.3);
    border-radius: 10px;
    margin: 0 auto;
    width: 50%;
    min-height: 36px;
  }
  .result {
    background: #ff6700;
    border-radius: 10px;
    width: 80%;
    height: 40px;
    margin: 0 auto;
    font-family: "Roboto";
    font-style: normal;
    font-weight: 900;
    font-size: 16px;
    line-height: 19px;
    color: #ffffff;
  }
  .rates {
    color: #ff6700;
    font-family: "Roboto";
    font-style: normal;
    font-weight: 300;
font-size: 16px;
line-height: 19px;
  }
  .ratesBottom {
    visibility: hidden;
    display: none;
  }
  .ratesTop {
    
    display: flex;
    margin: 0 auto;
    margin-top: 15px;
    width: 100%;
    justify-content: space-around;
  }
}
</style>