<template>
  <div class="hello">
    <div class="gerador">
      <h1>Gerador de feliz aniversário para Whatsapp</h1>
      <span>Quem está fazendo aniversário?</span>
      <input
        type="text"
        id="nome"
        placeholder="Nome do aniversariante"
        v-model="nome"
      />
      <button v-on:click="get_message(mensagens, nome)">
        {{ mensagem ? "Gerar outra mensagem" : "Gerar mensagem" }}
      </button>
    </div>
    <div v-if="mensagem" class="message">
      <h1>Mensagem</h1>
      <span id="msg_aniversario">{{ mensagem }}</span>
      <input type="hidden" id="text_msg" v-model="mensagem" />
      <button v-on:click="copiar()">
        {{ copiado ? "Copiado" : "Copiar" }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      mensagens: [
        "Parabéns #nome que Deus te conceda muitos anos de vida com saúde e paz.🎂👏🏻",
        "Parabéns #nome, que papai do céu te abençoe e te proteja hoje e sempre. Te amo ❤️🥰🥰",
        "Parabéns #nome, que Deus abençoe sua vida, e lhe dê muita saude e paz ! Felicidades , aproveite seu dia ! ❤️❤️👏🏻",
        "Feliz aniversario #nome! Que Deus te abençoe e lhe conceda muitos anos de vida e saúde.Felicidade e um dia especial.Um grande abraço 🥳🥳🥳🥳🥳👏🏽👏🏽👏🏽👏🏽👏🏽👏🏽",
        "Parabéns #nome muitas bençãos felicidades muita saúde e paz pra você Deus abençoe sempre🎂🎂🎂🎂🎂🎂🎂🎂🎂🎂🎂🥳🥳",
        "Parabéns #nome tudo de melhor na sua vida hoje e sempre , muita saúde e paz aproveita mto o seu dia 🎂🎂🎂👏👏👏👏",
        "Parabéns #nome,que Deus possa sempre te abençoar e iluminar seus caminhos e que continue sendo essa pessoa maravilhosa aproveita muito seu dia!!🥰🥰🥰🥰🥰❤️❤️❤️👏🏻👏🏻",
        "Parabéns #nome, toda felicidade do mundo, muita paz, saúde e tudo de melhor que existir, que Deus te abençoe e guie seus passos hoje e sempre!👏👏🎂🎂🎐🎐🎉🎉🎊🎊🙏🏻🙏🏻🎈🎈",
        "Parabéns #nome que nossa senhora te abençoe grandemente hoje e sempre, felicidades 🥳🥳👏👏👏",
        "Parabéns #nome que este dia seja repleto de bênçãos que Jesus e Maria te abençoe hoje e sempre! 🎊😘❤️🥳🎁🎂👏",
        "Parabéns e muitas felicidades #nome que seu dia seja lindo e especial como você!! 👏🏻🎂🥰🥰❤️🥳🥳",
        "Parabéns #nome tudo de melhor hoje e sempre ,muita saúde e sabedoria , felicidades🎂🎂🎂👏👏👏🥰🥰🥰",
        "Felicidades #nome que hoje no seu dia Jesus possa iluminar cada vez mais seus passos que vc continue sendo essa pessoa do bem e humildade sempre 💥⚡🍬🍦🎂😁😁😁",
        "Parabéns #nome que Jesus possa te abençoar sempre dando muita saúde, paz e sabedoria que você trilhe seus  caminhos na graça de Deus❤️👏👏🎂🎁🎉🥳❤️",
        "Parabéns #nome que Deus te conceda muitos anos de vida com saúde paz e muitas realizações !!🎂👏🏻👏🏻🥳🥰🥰",
        "Parabéns #nome. Que papai do céu te abençoe e te protege sempre. Que ele continue iluminando seus passos, para que você continue sendo esta pessoa de coração maravilhoso. Aproveita seu dia👏🏼👏🏼👏🏼❤️🥰🥰🥰🥰",
        "Parabéns #nome te desejo tudo de bom que há nesse mundo. Muitas felicidades e muitos anos de vida e saúde. Que Deus te abençoe e te proteja sempre",
        "Parabéns #nome, que Deus te ilumine e proteja sempre, que todos os seus sonhos se realizem e que você seja muito feliz. Tudo de bom para você hoje e sempre!👏🏻👏🏻❤️❤️❤️",
        "Parabéns #nome, muitos anos de vida e saúde e que nossa senhora ilumine você sempre feliz aniversário 👏👏👏😍🎉🎉🎉❤",
        "Parabéns #nome, toda felicidade do mundo, uma chuva de bençãos na sua vida, que Nossa Senhora e o Divino Espírito Santo te proteja e guie seus passos hoje e sempre!👏👏🎐🎐🎂🎂🎉🎉🎊🎊❤️❤️🥰🥰🥂🥂🎈🎈",
        "Parabéns #nome tudo de melhor hoje e sempre que nossa senhora te abençoe muito e te dê muitos anos de vida e saúde, felicidades 🎂🎂🎂👏👏👏👏🥰🥰🥰",
        "Parabéns #nome que Deus te proteja hoje e sempre você é muito especial de desejo tudo de bom 🥰🥰",
        "Parabéns #nome, que Deus te projeta hoje e sempre e lhe conceda muitas felicidades e bençãos. Aproveita seu dia 👏🏼👏🏼❤️🥰",
        "Parabéns #nome, que você continue sendo essa pessoa incrível e que Deus possa sempre te abençoar!!🥰🥰🥰🥰❤️❤️❤️👏🏻👏🏻🎉🎉🎉",
        "Parabéns #nome muitos anos de vida saúde e felicidade que Deus te abençoe com muita benção em sua vida🎂🎂🎂🎂🎂🎂🎂🎂🥳🥳🥳🥳🥳🥳🙏🏻🙏🏻🙏🏻",
        "Parabéns #nome muitos anos de vida saúde e paz na vida do senhor que Deus continue te iluminando 🥳🥳🥳🥳🥳🥳🥳🥳🥳🥳",
        "Feliz aniversário #nome, muitos anos de vida e saúde e que Deus te abençoe muito 🎂🎂🎂👏👏",
        "Parabéns e muitas felicidades #nome tudo de melhor hoje é sempre!!🎂👏👏😍",
        "Parabéns #nome tudo de melhor na sua vida hj e sempre, felicidades 👏👏👏🎂🎂🎂🎂🥰🥰🥰",
        "Feliz aniversário #nome, que Deus te abençoe. Aproveite muito seu dia e que ele seja cheio de bençãos e alegria. Que Deus lhe traga muitos anos de vida, alegria e saúde.",
        "Parabéns #nome, toda felicidade do mundo, uma chuva de bençãos na sua vida, que Deus te proteja e guie seus passos hoje e sempre! 👏👏🎂🎂🎐🎐🎊🎊🎈🎈🎉🎉",
        "Parabéns #nome felicidades muitos anos de vida muita saúde e paz que Nossa Senhora te cubra com seu manto sagrado 👏🏽🙌🏽🥳🥂💐",
        "Parabéns #nome, uma chuva de bençãos na sua vida, que Deus te proteja e guie seus passos hoje e sempre! 👏👏👏🎂🎂🎂",
        "Parabéns #nome tudo de bom felicidades que Deus abençoe sempre muita saúde paz tudo de bom🎂🎂🎂🎂🎂🎂🎂🥳🥳🥳🥳🥳🥳🥳🥳🥳🥳🥳🥳🥳❤️",
        "Parabéns e muitas felicidades #nome que Deus te conceda muitos anos de vida com saúde ,paz e muitas bênçãos. 👏🏻👏🏻🎂🥳🥳",
        "Parabéns #nome! Que Deus te abençoe e Nossa Senhora te proteja sempre. Muitas felicidades, saúde e paz👏🏽👏🏽👏🏽👏🏽👏🏽👏🏽👏🏽🥰🥰🥰🥰🥰🥳🥳🥳🥳",
      ],
      mensagem: "",
      nome: "",
      copiado: false,
    };
  },
  methods: {
    get_message(mensagens, nome) {
      let nova_mensagem = this.mensagem;
      while (nova_mensagem === this.mensagem) {
        nova_mensagem = mensagens[
          Math.floor(Math.random() * mensagens.length)
        ].replace("#nome", nome);
      }
      this.mensagem = nova_mensagem;
      this.copiado = false;
    },

    copiar() {
      let text_message = document.querySelector("#text_msg");
      text_message.setAttribute("type", "text");
      text_message.select();

      try {
        document.execCommand("copy");
        this.copiado = true;
      } catch (err) {
        console.log("Oops, unable to copy");
      }
      /* unselect the range */
      text_message.setAttribute("type", "hidden");
      window.getSelection().removeAllRanges();
    },
  },
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.gerador {
  display: flex;
  flex-direction: column;
  align-items: center;
  align-content: space-between;
  justify-content: center;
}

.gerador h1 {
  margin-bottom: 15px;
}

.gerador span {
  margin-bottom: 15px;
  font-size: 20px;
}

.gerador input {
  margin-bottom: 15px;
  padding: 10px;
  font-size: 20px;
  height: 30px;
  border: 1px solid #302e2e;
  border-radius: 10px;
  color: #302e2e;
}

.gerador button {
  margin-bottom: 15px;
  padding: 10px;
  height: 50px;
  width: 230px;
  border: 1px solid #302e2e;
  border-radius: 15px;
  font-size: 15px;
  background-color: #072b41;
  color: white;
}

.message span {
  margin-bottom: 15px;
  font-size: 20px;
  color: #302e2e;
}

.message button {
  margin-bottom: 15px;
  margin-left: 15px;
  padding: 10px;
  height: 40px;
  width: 100px;
  border: 1px solid #302e2e;
  border-radius: 15px;
  font-size: 15px;
  background-color: #072b41;
  color: white;
}
</style>
