<template>
  <div class="container mx-auto py-5 px-5">
    <div>
      <h3 class="text-2xl font-bold uppercase text-center mt-5">Tempo do</h3>
      <h3 class="text-4xl font-bold uppercase text-center">MAGAL</h3>
    </div>

    <div class="mx-auto mt-[150px]">
      <p class="text-center font-medium">Se eu falei que entro em
        <input type="number" v-model="minutos" @input="handleChangeTime" min="0" class="mx-2 px-2 w-20 border-sm">
        minuto(s)
      </p>
    </div>

    <div class="mx-auto mt-5">
      <Transition>
        <div v-if="phrase" class="text-center">
          <p class="font-medium">É porque eu quis dizer... <span class="text-xl  text-orange-400">{{ phrase }}</span>
          </p>
        </div>
      </Transition>
      
      <Transition name="pix">
        <div v-if="interactions > 5">
          <p class="text-center mt-[70px] font-medium">Gostou ? Que tal um</p>
          <p class="text-center font-medium leading-[0.7] text-[80px] text-emerald-400">PIX?</p>
        </div>
      </Transition>
    </div>
  </div>
</template>

<script setup>

const minutos = ref()
const phrase = ref()
const interactions = ref(0)

const randomPhrase = (value) => {
  phrase.value = null
  let possible_phares = []

  if (value >= 1 && value <= 5) {
    possible_phares = [
      "Já to indo... mais ou menos.",
      "Aquece uma que dá tempo!",
      "Só vou pegar água rapidinho.",
      "Segura aí, tô logando!",
      "Aguenta que já tô quase.",
      "Já tô com o dedo no Alt+Tab.",
      "Dois minutos e tô aí. Confia.",
      "Só um segundinho pra eu salvar o game aqui.",
      "Só vou fechar umas abas e já entro.",
      "Tô entrando... na fila pra logar.",
      "Só vou checar uma última coisa.",
      "Fica online, já tô quase!",
      "Um minutinho e já tô dentro.",
      "Pode contar até 60 que eu chego.",
      "Rapidinho mesmo, dessa vez é sério.",
      "Nem tira o headset que eu já volto.",
      "Só vou ajeitar meu setup e já entro.",
      "Mal comecei a demorar, segura aí.",
      "Relaxa, dessa vez vai ser rápido.",
      "Dei Alt+Tab errado, mas já volto!",
      "Espera só um instantinho!"
    ];
  }
  else if (value >= 6 && value <= 10) {
    possible_phares = [
      "Já dá tempo de um warm-up aí.",
      "Faz o tutorial que eu chego.",
      "Já volto, rapidinho. Prometo.",
      "Tô a caminho... do setup.",
      "Cinco minutinhos a mais, já volto.",
      "Vai dando ready aí, que eu já tô chegando.",
      "Só vou fazer um café pra acordar.",
      "Tô no loading... ainda.",
      "Entra aí na partida, eu chego no próximo round.",
      "Dois minutinho vira dez, mas juro que tô voltando!",
      "Dá pra configurar o mouse enquanto isso.",
      "Tô ajustando o headset, já entro.",
      "Vai dando a call que eu já pego no meio.",
      "É só um cafezinho, rapidinho!",
      "Espera só mais cinco minutinhos...",
      "Se começar sem mim, eu te entendo.",
      "Tô atualizando uns plugins, quase pronto.",
      "Vai fazendo um pre-game aí!",
      "Estou resolvendo uma coisa rápida.",
      "Vou pegar o teclado novo e já volto."
    ];
  }
  else if (value >= 11 && value <= 15) {
    possible_phares = [
      "Dá pra você jogar uma enquanto isso.",
      "Pode aquecer, hoje eu chego devagar.",
      "Tô só esperando carregar os drivers aqui.",
      "Dá pra assistir um episódio enquanto eu venho.",
      "O sistema tá atualizando, mas eu entro logo.",
      "Vou tomar um café, mas depois disso tô pronto.",
      "Abre uma sala e vai treinando que eu já tô por aí.",
      "Prometi 5, mas deve ser uns 15... Já já eu entro!",
      "Caiu a internet, mas eu já tô voltando.",
      "Pode ir jogando, na próxima eu tô!",
      "Desce uma partida e já vou!",
      "Só mais alguns ajustes técnicos aqui.",
      "Dá tempo de escolher o personagem enquanto isso.",
      "Tô resolvendo uma treta rápida, aguenta aí.",
      "Pode deixar a fila rodar, eu já entro.",
      "Abre aí que eu só tô me conectando!",
      "Vou fechar uns programas antes de entrar.",
      "Tá carregando uns 300 MB, já chego.",
      "Tô ajustando as configurações, calma.",
      "Pode começar que na próxima eu tô!"
    ];
  }
  else if (value >= 16 && value <= 30) {
    possible_phares = [
      "Dá tempo de ir buscar comida, relaxa.",
      "Dá pra assistir um filminho e eu apareço no final.",
      "Tô esperando a fila, vai demorar mais um pouquinho.",
      "Dá tempo de lavar a louça e ainda sobra.",
      "Vou fazer um lanche, mas depois disso tô pronto.",
      "Vai jogando, tô preso numa call aqui.",
      "Espera um pouquinho mais... já chego!",
      "Minha placa de vídeo decidiu atualizar agora...",
      "Calma aí, a instalação tá quase terminando!",
      "Ainda na fila pra entrar no server. Vai mais uns minutinhos.",
      "Dá pra dar uma saída rápida e voltar.",
      "Espera só, tenho que reiniciar o PC.",
      "A fila tá enorme, vai levar mais um pouco.",
      "Acho que vou pedir comida enquanto espero.",
      "Pode jogar sem mim, que ainda demora um pouco.",
      "Só mais alguns updates e já chego.",
      "Tô fazendo um lanche rápido, quase pronto.",
      "Aguenta aí, preciso reinstalar umas coisas.",
      "Dá pra assistir um vídeo enquanto isso.",
      "Tô no meio de uma missão, mas já volto."
    ];
  }
  else if (value >= 31) {
    possible_phares = [
      "Dá tempo de você fazer uma janta completa.",
      "Vai fazer a academia que eu apareço depois!",
      "Tá com tempo? Porque vai demorar!",
      "Cafézinho, lavar a louça e depois senta que eu apareço.",
      "Já dá pra maratonar uma série e eu ainda não entro.",
      "Levo tanto tempo que dá pra trocar de jogo.",
      "Pede um lanche e vai comendo enquanto espera!",
      "Já tô na metade do caminho... acho.",
      "Vai dormir e amanhã eu apareço no lobby.",
      "Pode jogar a temporada toda que eu entro no final.",
      "Troca de console, que até lá eu entro.",
      "Vai jogar outro jogo enquanto eu apareço.",
      "Já era pra eu ter chegado, mas ainda tô vindo.",
      "Aguenta mais um pouco... talvez muito pouco.",
      "Pode lavar a louça e fazer a janta enquanto isso.",
      "Dá pra organizar a casa e ainda sobrar tempo.",
      "Já virei meme de tanto tempo que demoro.",
      "Eu avisei que ia demorar, mas talvez eu tenha exagerado.",
      "Pode virar o dia jogando, talvez eu apareça.",
      "Faz qualquer coisa, que eu chego quando você menos esperar."
    ];
  }

  const randomIndex = Math.floor(Math.random() * possible_phares.length);
  return possible_phares[randomIndex];
}

const handleChangeTime = (e) => {
  const value = e.target.value
  phrase.value = randomPhrase(value)
  interactions.value += 1
}

useHead({
  title: 'Tempo do Magal - Quando eu realmente vou entrar?',
  meta: [
    // SEO básico
    { name: 'description', content: 'Descubra a verdadeira conversão do tempo de espera que eu disse que ia entrar!' },
    { name: 'keywords', content: 'tempo de espera, conversão de tempo, memes, tempo do Magal' },
    { name: 'robots', content: 'index, follow' }, // Para SEO: permitir indexação e seguir links
    { name: 'viewport', content: 'width=device-width, initial-scale=1' },

    // Open Graph (OG)
    { property: 'og:title', content: 'Tempo do Magal - Quando eu realmente vou entrar?' },
    { property: 'og:description', content: 'Converta o tempo de espera que você acha que ia entrar e veja quanto realmente demorou!' },
    { property: 'og:image', content: 'https://w0.peakpx.com/wallpaper/327/568/HD-wallpaper-pubg-illustration-art-fan-game-work.jpg' }, // Substitua pelo URL correto
    { property: 'og:url', content: 'https://tempo-do-magal.vercel.app/' }, // Substitua pelo seu domínio
    { property: 'og:type', content: 'website' },

    // Twitter Cards
    { name: 'twitter:card', content: 'summary_large_image' }, // Exibe uma imagem grande no card do Twitter
    { name: 'twitter:title', content: 'Tempo do Magal - Quando eu realmente vou entrar?' },
    { name: 'twitter:description', content: 'Converta o tempo de espera que você acha que ia entrar e veja quanto realmente demorou!' },
    { name: 'twitter:image', content: 'https://w0.peakpx.com/wallpaper/327/568/HD-wallpaper-pubg-illustration-art-fan-game-work.jpg' }, // Substitua pelo URL correto
  ],
  link: [
    { rel: 'canonical', href: 'https://tempo-do-magal.vercel.app/' } // Link canonical para SEO
  ]
});

</script>

<style>
html {
  @apply bg-slate-200;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.pix-enter-active,
.pix-leave-active {
  transition: opacity 2.5s ease;
}

.pix-enter-from,
.pix-leave-to {
  opacity: 0;
}
</style>