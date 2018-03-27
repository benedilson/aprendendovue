<template>
  <div>
    <h1 class="centralizado">{{ titulo }}</h1>

    <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="filtre por parte do titulo">
    
    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosComFiltro" :key="foto.id">
        <meu-painel :titulo="foto.titulo">
        <!-- imagem-responsiva v-meu-transform.animacao.reverse="15" :url="foto.url" :titulo="foto.titulo"/> -->
        <!-- imagem-responsiva v-meu-transform.animacao="15" :url="foto.url" :titulo="foto.titulo"/> -->
        <!-- imagem-responsiva v-meu-transform:rotate.animacao="15" :url="foto.url" :titulo="foto.titulo"/> -->
            <imagem-responsiva v-meu-transform:scale.animacao="1.2" :url="foto.url" :titulo="foto.titulo"/>
            
            <!--confirmacao e estilo podem ser omitidos -->
            <meu-botao 
              tipo="button" 
              rotulo="REMOVER" 
              @botaoAtivado="remove(foto)"
              :confirmacao="true"
              estilo="padrao" />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>

import Painel from '../shared/painel/Painel.vue';
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue';
import Botao from '../shared/botao/Botao.vue';

export default {

  components: {
    'meu-painel' : Painel,
    'imagem-responsiva': ImagemResponsiva,
    'meu-botao' : Botao
  },

  data() {
    return {
      titulo: 'Jogos do Super Nintendo',
      fotos: [
        {
          url: 'https://static.vix.com/pt/sites/default/files/styles/large/public/bbr/super-mario-world.jpg?itok=aHOy3Q4Y',
          titulo: 'mario'
        },
        {
          url: 'http://gamehall.uol.com.br/v10/wp-content/uploads/2013/01/maxresdefault-3-790x444.jpg',
          titulo: 'biker mice from mars'
        },
        {
          url: 'https://i.pinimg.com/originals/5a/02/93/5a02939e6d846f6e938f90c20018a2d6.jpg',
          titulo: 'MK3'
        },
        {
          url: 'http://3.bp.blogspot.com/-HVjSCEmLgXQ/T3xcsswmUEI/AAAAAAAAAj0/d6zZes5I8Wg/s1600/mmx2.jpg',
          titulo: 'megaman x2'
        },
        {
          url: 'http://gamehall.uol.com.br/v10/wp-content/uploads/2010/04/2364793-snes_streetfighterii-790x578.jpg',
          titulo: 'Street Fight II'
        },
        {
          url: 'https://i.pinimg.com/originals/4f/bf/50/4fbf50de536c807a7c066cc952467224.jpg',
          titulo: 'Super Bomberman 4'
        },
        {
          url: 'https://upload.wikimedia.org/wikipedia/fi/7/70/Goof_troop.jpg',
          titulo: 'Goof Troop'
        },
        {
          url: 'http://1.bp.blogspot.com/_4TStK8uZrgU/TETacktTyYI/AAAAAAAAFB4/RjJqSs2n_gw/s400/dk_country_2.jpg',
          titulo: 'Donkey Kong 2'
        },
        {
          url: 'http://gamehall.uol.com.br/v10/wp-content/uploads/2010/08/Final_Fight_3-790x577.jpg',
          titulo: 'Final Fight 3'
        },
        {
          url: 'http://contemgames.com.br/imagens/Games/1995-International-Superstar-Soccer-1.jpg',
          titulo: 'International Superstar Soccer'
        },
        {
          url: 'http://www.mobygames.com/images/covers/l/246841-the-adventures-of-batman-robin-snes-front-cover.jpg',
          titulo: 'The Adventures of Batman & Robin'
        },
        {
          url: 'https://joysticknervoso.files.wordpress.com/2014/09/top-gear3000-fita1.jpg',
          titulo: 'Top Gear 3000'
        }
      ],
      filtro: ''
    }
  },

  computed: {
    fotosComFiltro() {
      if(this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      }
      else {
        return this.fotos;
      }
    }
  },

  methods: {
    remove(foto) {
        alert('Remover a foto! ' + foto.titulo);
    }
  },

  /*
  created() {
    this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, err => console.log(err));
  }
  */
}
</script>

<style>
  .centralizado {
    text-align: center;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos-item {
    display: inline-block;
  }

  .filtro {
    display: block;
    width: 100%;
  }

</style>
