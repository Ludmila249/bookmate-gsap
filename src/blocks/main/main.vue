<template>
  <div class="page">
    <header class="page__header">
      <img src="../../images//logo.svg" alt="" />
      <ul class="page__menu">
        <li v-for="item in menu" :key="item.name">
          <div class="page__menu-button" @click="scrollLink(item.scrollDesktop)">
            {{ item.name }}
          </div>
        </li>
      </ul>
      <button class="page__link" @click="scrollContact">Наши контакты</button>
      <button class="page__button-burger" @click="openMenuMobile">
        <span class="page__burger" />
      </button>
    </header>
    <div :class="bem('page__menu-mobile-wrap', { openMenu })" @click.self="closeMenuMobile">
      <ul :class="bem('page__menu-mobile', { openMenu })">
        <button class="page__button-burger page__button-burger_close" @click="closeMenuMobile">
          <span class="page__burger page__burger_close" />
        </button>
        <li v-for="item in menu" :key="item.name">
          <div class="page__menu-item" @click="scrollLink(item.scrollMobile)">{{ item.name }}</div>
        </li>
        <a class="page__mobile-link" @click="scrollContact">Наши контакты</a>
      </ul>
    </div>
    <div id="smooth-wrapper">
      <div id="smooth-content">
        <div ref="start" class="page__block-animation">
          <div ref="title" class="page__block-title">
            <p class="page__title">
              Букмейт<br />
              издательствам и&nbsp;писателям
            </p>
          </div>
          <div id="problem" ref="problem" class="page__block-problem block-problem">
            <h2 class="block-problem__title">Проблема</h2>
            <p class="block-problem__text">90% аудиокниг не озвучиваются по разным причинам</p>
            <ul>
              <li v-for="elem in problem" :key="elem.number" class="block-problem__item">
                <p class="block-problem__bullitt">{{ elem.number }}</p>
                <div>
                  <p class="block-problem__item-title">{{ elem.title }}</p>
                  <p class="block-problem__item-text">{{ elem.text }}</p>
                </div>
              </li>
            </ul>
          </div>
          <div ref="solution" class="page__block-solution block-solution">
            <img ref="solutionBg" class="block-solution__bg" src="../../images/bg.png" alt="" />
            <h2 id="solution" ref="solutionTitle" class="block-solution__title">Решение</h2>
            <p ref="solutionText" class="block-solution__text">
              Мы&nbsp;сделали модель озвучки специально разработанную для книг, чтобы сохранить
              привычные интонации и&nbsp;уникальный характер каждого произведения
            </p>
            <h2 ref="titleTwoChapter" class="block-solution__title-two-chapter">Послушайте</h2>
            <div ref="blockProfessionals" class="page__block-professionals block-professionals">
              <img
                ref="blockProfessionalsSound"
                class="block-professionals__sound"
                src="../../images/sound.svg"
                alt=""
              />
              <div
                id="protection"
                ref="blockProfessionalsText"
                class="block-professionals__text-wrap"
              >
                <p ref="professionalsText" class="block-professionals__text">
                  Мы не&nbsp;<nobr>убиваем</nobr> <nobr>работу</nobr> <nobr>чтеца</nobr> и
                  <nobr>не</nobr>&nbsp;<nobr>крадем</nobr> <nobr>голоса.</nobr> <nobr>Нам</nobr>
                  <nobr>доверились</nobr> <nobr>уже</nobr> <nobr>120</nobr>
                  <nobr>профессиональных</nobr>
                  <nobr>дикторов</nobr>
                </p>
              </div>
            </div>
            <div
              id="cooperation"
              ref="cooperation"
              class="page__block-cooperation block-cooperation"
            >
              <h2 ref="cooperationTitle">
                Давайте же<br />
                сотрудничать
              </h2>
              <div ref="cooperationText" class="block-cooperation__wrap-contact">
                <p class="block-cooperation__text">hello@bmate.ru</p>
                <svg
                  ref="svgAnimation"
                  xmlns="http://www.w3.org/2000/svg"
                  width="1281"
                  height="289"
                  viewBox="0 0 1281 289"
                  fill="none"
                >
                  <path
                    id="path"
                    d="M1064.37 246.506C829.406 277.888 302.076 310.74 72.4664 191.092C-214.546 41.532 625.914 3.77152 946.913 15.8807C1138.98 23.1259 1265.5 54.54 1267.6 107.202C1269.4 152.54 1054.94 229.337 661.357 232.124"
                    stroke="#BAD131"
                    stroke-width="25.7707"
                    stroke-linecap="round"
                  />
                </svg>
              </div>
              <img
                ref="cooperationBg"
                class="block-cooperation__img"
                src="../../images//bg-end.png"
                alt=""
              />
            </div>
            <div ref="announcers" class="block-cooperation__announcers announcers">
              <div v-for="item in announcers" :key="item.index" class="announcers__card-announcers">
                <img :src="item.src" alt="" />
                <p v-html="item.name" />
              </div>
            </div>
            <div id="voiceover" ref="dubbing" class="block-professionals__dubbing">
              <div class="block-professionals__option-dubbing">
                <p>Озвучка 1</p>
                <span />
              </div>
              <div class="block-professionals__option-dubbing">
                <p>Озвучка 2</p>
                <span />
              </div>
              <div class="block-professionals__option-dubbing">
                <p>Озвучка 3</p>
                <span />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { gsap } from '../../lib/gsap';
import { ScrollTrigger } from '../../lib/gsap/ScrollTrigger';
import { ScrollSmoother } from '../../lib/gsap/ScrollSmoother';
import { ScrollToPlugin } from '../../lib/gsap/ScrollToPlugin';
import { SplitText } from '../../lib/gsap/SplitText';
import { DrawSVGPlugin } from '../../lib/gsap/DrawSVGPlugin';

export default {
  name: 'main-block',
  data() {
    return {
      smoother: null,
      openMenu: false,
      menu: [
        {
          name: 'Проблема',
          link: '#problem',
          scrollDesktop: 150,
          scrollMobile: 90,
        },
        {
          name: 'Решение',
          link: '#solution',
          scrollDesktop: 2300,
          scrollMobile: 720,
        },
        {
          name: 'Пример озвучки',
          link: '#voiceover',
          scrollDesktop: 3200,
          scrollMobile: 2100,
        },
        {
          name: 'Защита',
          link: '#protection',
          scrollDesktop: 5000,
          scrollMobile: 2900,
        },
      ],
      problem: [
        {
          number: 1,
          title: 'Ограниченные ресурсы',
          text: 'Озвучка аудиокниг требует значительных ресурсов, включая время, деньги и техническое оборудование. Не все издатели или авторы могут себе позволить инвестировать в процесс озвучки',
        },
        {
          number: 2,
          title: 'Авторские права',
          text: 'Некоторые книги имеют ограничения на создание аудиоверсий из-за сложностей в получении или урегулировании авторских прав',
        },
        {
          number: 3,
          title: 'Недостаток спроса',
          text: 'Некоторые издатели или авторы могут не видеть достаточного спроса на аудиокниги для определенных жанров или категорий, поэтому они не приоритезируют озвучку',
        },
        {
          number: 4,
          title: 'Технические сложности',
          text: 'Озвучка книг может быть трудной из-за сложности переноса письменного текста на звук. Это требует профессиональных дикторов, студийной техники и специализированного редактирования аудио',
        },
        {
          number: 5,
          title: 'Локализация',
          text: 'Книги на разных языках и диалектах требуют различных озвучиваний, чтобы соответствовать конкретным культурным и языковым нюансам, что может создавать дополнительные сложности и затраты',
        },
      ],
      announcers: [
        {
          name: 'Леонид<br/> Заполярный',
          src: '/static/avatar-1.jpg',
        },
        {
          name: 'Леонид Заполярный',
          src: '/static/avatar-2.jpg',
        },
        {
          name: 'Леонид Заполярный',
          src: '/static/avatar-3.jpg',
        },
        {
          name: 'Леонид Заполярный',
          src: '/static/avatar-4.jpg',
        },
      ],
    };
  },
  watch: {
    // openMenu(value) {
    //   this.scrollLock(value);
    // },
    solutionBlock(value) {
      this.heightBlockText = value;
    },
  },
  mounted() {
    this.smootherSetup();
    gsap.registerPlugin(ScrollTrigger);
    gsap.registerPlugin(SplitText);
    gsap.registerPlugin(ScrollToPlugin);
    gsap.registerPlugin(DrawSVGPlugin);
    const mm = gsap.matchMedia();
    mm.add('(min-width: 1024px)', this.scrollAnimationDesktop);
    mm.add('(max-width: 1023px)', this.scrollAnimationMobile);
  },
  methods: {
    scrollAnimationDesktop() {
      const mySplitText = new SplitText(this.$refs.professionalsText, { type: 'chars' });
      const { chars } = mySplitText;

      const scrollTl = gsap.timeline({
        scrollTrigger: {
          trigger: this.$refs.start,
          start: 'top top',
          end: '+=10000px',
          scrub: 5,
          pin: true,
        },
      });

      gsap.set(this.$refs.problem, {
        top: 0,
        y: '+93vh',
      });
      gsap.set(this.$refs.solution, {
        y: '88vh',
        top: 0,
      });
      gsap.set(this.$refs.solutionBg, {
        top: 0,
      });
      gsap.set(this.$refs.solutionText, {
        y: '+100vh',
      });
      gsap.set(this.$refs.titleTwoChapter, {
        y: '+100vh',
      });
      gsap.set(this.$refs.blockProfessionals, {
        y: '+100vh',
        zIndex: 5,
      });
      gsap.set(this.$refs.dubbing, {
        y: '+100vh',
      });
      gsap.set(this.$refs.blockProfessionalsText, {
        y: '+130vh',
      });
      gsap.set(this.$refs.professionalsText, {
        perspective: 400,
      });
      gsap.set(chars, {
        opacity: 0.4,
      });
      gsap.set(this.$refs.announcers, {
        x: '+100vw',
        left: 0,
      });
      gsap.set(this.$refs.cooperation, {
        y: '+130vh',
      });
      gsap.set(this.$refs.cooperationTitle, {
        y: '+120vh',
      });
      gsap.set(this.$refs.cooperationText, {
        y: '+120vh',
      });
      gsap.set(this.$refs.svgAnimation, {
        y: '14vh',
      });
      gsap.set('#path', {
        drawSVG: '0%',
        stagger: 0.1,
      });
      gsap.set(this.$refs.cooperationBg, {
        y: '20vh',
      });

      // вылет блока проблем
      scrollTl.to(this.$refs.problem, {
        y: '-150vh',
        duration: 5,
      });
      scrollTl.to(
        this.$refs.solution,
        {
          transform: 'translate(0px, calc((100vh - 540px) / 2))',
          duration: 1.1,
        },
        '<',
      );
      scrollTl.to(
        this.$refs.title,
        {
          opacity: 0,
        },
        '<+=1',
      );
      scrollTl.to(
        this.$refs.solutionBg,
        {
          display: 'block',
        },
        '>',
      );
      scrollTl.to(this.$refs.solution, {
        y: 0,
        top: 0,
        width: '100%',
        height: '100vh',
        borderRadius: 0,
        duration: 2,
      });
      scrollTl.to(
        this.$refs.solutionBg,
        {
          duration: 2,
          width: '900px',
        },
        '<',
      );
      scrollTl.to(this.$refs.solutionTitle, {
        transform: 'scale(0.4)',
        opacity: '0.6',
        duration: 2,
        delay: 1,
      });
      scrollTl.to(this.$refs.solutionText, {
        y: '+40vh',
        opacity: 1,
        duration: 3,
        delay: 2,
      });
      scrollTl.to(
        this.$refs.solutionTitle,
        {
          y: '-15vh',
          duration: 2,
        },
        '<',
      );
      // исчезновение текста
      scrollTl.to(this.$refs.solutionTitle, {
        y: '-50vh',
        opacity: 0,
        delay: 3,
      });
      scrollTl.to(
        this.$refs.solutionText,
        {
          y: '0',
          opacity: '0',
        },
        '<',
      );
      scrollTl.to(
        this.$refs.solutionBg,
        {
          y: '-20vh',
          opacity: '0',
        },
        '<',
      );
      scrollTl.to(this.$refs.titleTwoChapter, {
        y: '+25vh',
        opacity: '1',
      });
      scrollTl.to(this.$refs.blockProfessionals, {
        y: '45vh',
        delay: 1,
      });
      scrollTl.to(this.$refs.dubbing, {
        y: '35vh',
        zIndex: 9,
      });
      scrollTl.to(
        this.$refs.titleTwoChapter,
        {
          delay: 2,
          y: '-20vh',
          opacity: '0',
        },
        '<+=1',
      );
      scrollTl.to(this.$refs.blockProfessionals, {
        borderRadius: '240px',
        duration: 2,
        width: '100%',
      });
      scrollTl.to(
        this.$refs.blockProfessionalsSound,
        {
          width: '80%',
        },
        '<',
      );
      scrollTl.to(
        this.$refs.blockProfessionals,
        {
          display: 'block',
          duration: 4,
          height: '160vh',
        },
        '<',
      );
      scrollTl.to(
        this.$refs.blockProfessionals,
        {
          y: '-30vh',
          duration: 2,
        },
        '<+=2',
      );
      scrollTl.to(
        this.$refs.dubbing,
        {
          y: '-70vh',
          duration: 3,
        },
        '<',
      );
      scrollTl.to(
        this.$refs.blockProfessionalsText,
        {
          duration: 3,
          // transform: 'translate(0px, calc((160vh - 427px) / 2))',
          y: '57vh',
        },
        '< += 0.5',
      );
      scrollTl.to(
        this.$refs.blockProfessionalsSound,
        {
          y: '-10vh',
          duration: 3,
        },
        '<',
      );
      scrollTl.to(this.$refs.solution, {
        backgroundColor: '#000',
      });
      // анимация букв
      scrollTl.to(
        chars,
        {
          duration: 0.1,
          opacity: 1,
          stagger: 0.1,
        },
        '<+=0.5',
      );
      scrollTl.to(this.$refs.announcers, {
        bottom: '120px',
      });
      scrollTl.to(this.$refs.blockProfessionalsText, {
        y: '-200vh',
        duration: 10,
      });
      scrollTl.to(
        this.$refs.announcers,
        {
          x: '-100vw',
          duration: 10,
        },
        '< += 0.2',
      );
      scrollTl.to(
        this.$refs.blockProfessionals,
        {
          y: '-120vh',
          height: '120vh',
          duration: 10,
        },
        '<+=6',
      );
      scrollTl.to(
        this.$refs.solution,
        {
          backgroundColor: '#0E664B',
        },
        '<',
      );
      scrollTl.to(
        this.$refs.cooperation,
        {
          height: '110vh',
          duration: 4,
          y: '0vh',
          zIndex: 0,
        },
        '<',
      );
      scrollTl.to(
        this.$refs.cooperationTitle,
        {
          y: '0vh',
          duration: 8,
        },
        '<+=1',
      );
      scrollTl.to(this.$refs.cooperationTitle, {
        y: '-15vh',
        transform: 'scale(0.3)',
        opacity: '0.6',
        duration: 4,
      });
      scrollTl.to(
        this.$refs.cooperationText,
        {
          y: '-19vh',
          duration: 8,
          zIndex: 6,
        },
        '<',
      );
      scrollTl.to(this.$refs.svgAnimation, {
        y: '-4vh',
      });
      scrollTl.to('#path', {
        duration: 5,
        drawSVG: '100%',
        stagger: 0.1,
      });
      scrollTl.to(
        this.$refs.cooperationBg,
        {
          width: '100%',
          duration: 5,
          y: '13vh',
        },
        '<',
      );
    },
    scrollAnimationMobile() {
      const mySplitText = new SplitText(this.$refs.professionalsText, { type: 'chars' });
      const { chars } = mySplitText;

      const scrollTl = gsap.timeline({
        scrollTrigger: {
          trigger: this.$refs.start,
          start: 'top top',
          end: '+=6700px',
          scrub: 10,
          pin: true,
        },
      });

      gsap.set(this.$refs.problem, {
        y: '89vh',
        top: 0,
      });
      gsap.set(this.$refs.solution, {
        y: '85vh',
        minHeight: '424px',
        top: 0,
      });
      gsap.set(this.$refs.solutionBg, {
        width: '318px',
      });
      gsap.set(this.$refs.solutionText, {
        y: '+100vh',
      });
      gsap.set(this.$refs.titleTwoChapter, {
        y: '+100vh',
      });
      gsap.set(this.$refs.blockProfessionals, {
        height: 'auto',
        y: '+100vh',
        zIndex: 5,
      });
      gsap.set(this.$refs.dubbing, {
        y: '+100vh',
      });
      gsap.set(this.$refs.blockProfessionalsText, {
        y: '+130vh',
      });
      gsap.set(this.$refs.professionalsText, {
        perspective: 400,
      });
      gsap.set(chars, {
        opacity: 0.4,
      });
      gsap.set(this.$refs.announcers, {
        x: '+100vw',
        left: 0,
        bottom: '150px',
      });
      gsap.set(this.$refs.cooperation, {
        y: '+130vh',
        bottom: 0,
      });
      gsap.set(this.$refs.cooperationTitle, {
        y: '+120vh',
      });
      gsap.set(this.$refs.cooperationText, {
        y: '+120vh',
      });
      gsap.set(this.$refs.svgAnimation, {
        y: '14vh',
      });
      gsap.set('#path', {
        drawSVG: '0%',
        stagger: 0.1,
      });

      scrollTl.to(this.$refs.solution, {
        transform: 'translate(0px, calc((100vh - 540px) / 2))',
        duration: 1,
      });
      scrollTl.to(
        this.$refs.problem,
        {
          y: '-150vh',
          duration: 3,
        },
        '<',
      );
      scrollTl.to(
        this.$refs.solutionBg,
        {
          display: 'block',
        },
        '<+=0.1',
      );
      scrollTl.to(this.$refs.solution, {
        y: 0,
        width: '100%',
        height: '100vh',
        borderRadius: 0,
        duration: 1,
      });
      scrollTl.to(this.$refs.solutionBg, {
        width: '100%',
      });
      scrollTl.to(this.$refs.solutionTitle, {
        transform: 'scale(0.7)',
        y: '-15vh',
        opacity: '0.6',
      });
      scrollTl.to(
        this.$refs.solutionText,
        {
          y: '40vh',
          opacity: 1,
        },
        '<',
      );
      scrollTl.to(this.$refs.solutionTitle, {
        y: '-60vh',
        duration: 1,
        delay: 5,
      });
      scrollTl.to(
        this.$refs.solutionText,
        {
          y: '-50vh',
          duration: 2,
        },
        '<',
      );
      scrollTl.to(
        this.$refs.titleTwoChapter,
        {
          y: '32vh',
          opacity: 1,
          duration: 1,
        },
        '<+=1',
      );
      scrollTl.to(this.$refs.blockProfessionals, {
        height: 'auto',
      });
      scrollTl.to(this.$refs.blockProfessionals, {
        y: '50vh',
        opacity: 1,
        duration: 1,
      });
      scrollTl.to(this.$refs.dubbing, {
        y: '30vh',
        zIndex: 8,
      });
      scrollTl.to(this.$refs.titleTwoChapter, {
        y: '-40vh',
        delay: 1,
      });
      scrollTl.to(this.$refs.blockProfessionals, {
        display: 'block',
        y: '-15vh',
        width: '100%',
        borderRadius: '50px',
      });
      scrollTl.to(
        this.$refs.blockProfessionals,
        {
          height: '130vh',
        },
        '<+=0.3',
      );
      scrollTl.to(this.$refs.blockProfessionalsSound, {
        y: '-50vh',
      });
      scrollTl.to(this.$refs.dubbing, {
        y: '-120vh',
        duration: '2',
      });
      scrollTl.to(
        this.$refs.blockProfessionalsText,
        {
          y: '50vh',
        },
        '<+=0.5',
      );
      scrollTl.to(
        chars,
        {
          duration: 0.1,
          opacity: 1,
          stagger: 0.1,
        },
        '<+=0.5',
      );
      scrollTl.to(this.$refs.blockProfessionalsText, {
        y: '-50vh',
        duration: 4,
      });
      scrollTl.to(
        this.$refs.announcers,
        {
          x: '-250vw',
          duration: 6,
        },
        '<+=0.5',
      );
      scrollTl.to(
        this.$refs.blockProfessionals,
        {
          y: '-140vh',
          duration: 8,
        },
        '<+=2',
      );
      scrollTl.to(
        this.$refs.cooperation,
        {
          height: '100vh',
          duration: 2,
          y: '0vh',
          zIndex: 0,
        },
        '<',
      );
      scrollTl.to(
        this.$refs.cooperationTitle,
        {
          y: '10vh',
          duration: 5,
        },
        '<+=1',
      );
      scrollTl.to(this.$refs.cooperationTitle, {
        y: '-10vh',
        transform: 'scale(0.5)',
        opacity: 0.6,
        duration: 2,
      });
      scrollTl.to(this.$refs.cooperationText, {
        y: '-13vh',
        zIndex: 6,
      });
      scrollTl.to(this.$refs.svgAnimation, {
        width: '100%',
        left: 0,
        y: '-1vh',
        bottom: 0,
      });
      scrollTl.to('#path', {
        duration: 5,
        drawSVG: '100%',
        stagger: 0.1,
      });
      scrollTl.to(
        this.$refs.cooperationBg,
        {
          width: '100%',
          duration: 5,
          y: '7vh',
          delay: 2,
        },
        '<',
      );
    },
    scrollLink(scroll) {
      if (this.smoother) {
        gsap.to(window, { duration: 1, scrollTo: scroll });
      } else {
        gsap.to(window, { duration: 1, scrollTo: scroll });
        this.openMenu = false;
      }
    },
    scrollContact() {
      gsap.to(window, { duration: 1, scrollTo: 10000 });
      this.openMenu = false;
    },
    smootherSetup() {
      gsap.registerPlugin(ScrollTrigger);
      gsap.registerPlugin(ScrollSmoother);
      const userAgent = navigator.userAgent.toLowerCase();
      const isAndroid = userAgent.indexOf('android') > -1;
      const isIos = /iphone|ipad|ipod/.test(userAgent);

      if (isAndroid) {
        ScrollTrigger.config({
          ignoreMobileResize: true,
        });
        ScrollTrigger.normalizeScroll(true);
      } else if (isIos) {
        ScrollTrigger.config({
          ignoreMobileResize: false,
        });
        ScrollTrigger.normalizeScroll(false);
      } else {
        this.smoother = ScrollSmoother.create({
          smooth: 2,
          effects: true,
          ignoreMobileResize: true,
          normalizeScroll: true,
        });
      }
    },
    openMenuMobile() {
      this.openMenu = true;
    },
    closeMenuMobile() {
      this.openMenu = false;
    },
    scrollLock(status) {
      // eslint-disable-next-line no-unused-expressions
      status
        ? document.querySelector('html').classList.add('scroll-lock')
        : document.querySelector('html').classList.remove('scroll-lock');
    },
  },
};
</script>

<style src="./main.less" lang="less"></style>
