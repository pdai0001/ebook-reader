<template>
  <div class="shelf-empty-bg-wrapper">
    <span class="btn-text" @click="switchLocale">{{ $t('shelf.changeLanguage') }}</span>
    <div class="book-shelf-empty-wrapper" ref="emptyView">
      <div class="empty-img-wrapper">
        <img class="empty-img" :src="img">
      </div>
      <div class="empty-text-wrapper">
        <div class="empty-text" v-html="$t('shelf.welcome')"></div>
      </div>
      <div class="empty-btn-wrapper">
        <div class="empty-btn" @click="gotoStudy">{{ $t('shelf.studyNow') }}</div>
        <div class="empty-btn" @click="gotoBookStore">{{ $t('shelf.find') }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { realPx } from '../../utils/utils'
import { setLocalStorage } from '../../utils/localStorage'
import { storeShelfMixin } from '../../utils/mixin'

export default {
  mixins: [storeShelfMixin],
  data () {
    return {
      img: require('@/assets/images/panda.jpg')
    }
  },
  computed: {
    lang () {
      return this.$i18n.locale
    }
  },
  methods: {
    gotoBookStore () {
      this.$router.push('/store/home')
    },
    gotoStudy () {
      this.$router.push('/store')
    },
    switchLocale () {
      if (this.lang === 'en') {
        this.$i18n.locale = 'cn'
      } else {
        this.$i18n.locale = 'en'
      }
      setLocalStorage('locale', this.$i18n.locale)
    }
  },
  mounted () {
    this.$refs.emptyView.style.height = window.innerHeight - realPx(42) + 'px'
  }
}
</script>

<style lang="scss" scoped>
  @import "../../assets/styles/global";
  .btn-text {
    position: absolute;
    top: px2rem(8);
    right: px2rem(8);
    font-size: px2rem(16);
    color: #333;
    line-height: px2rem(30);
  }
  .book-shelf-empty-wrapper {
    width: 100%;
    .empty-img-wrapper {
      width: 100%;
      margin-top: px2rem(50);
      text-align: center;
      .empty-img {
        width: px2rem(200);
        height: px2rem(200);
      }
    }
    .empty-text-wrapper {
      width: 100%;
      margin-top: px2rem(10);
      text-align: center;
      padding: 0 px2rem(15);
      box-sizing: border-box;
      .empty-text {
        font-size: px2rem(16);
        color: #333;
        line-height: px2rem(30);
      }
    }
    .empty-btn-wrapper {
      width: 100%;
      padding: px2rem(30) px2rem(15) px2rem(15) px2rem(15);
      box-sizing: border-box;
      @include center;
      .empty-btn {
        width: 100%;
        font-size: px2rem(14);
        font-weight: bold;
        color: white;
        padding: px2rem(15) 0;
        text-align: center;
        border-radius: px2rem(10);
        background: $color-blue;
        &:first-child {
          margin-right: px2rem(7.5);
          background: #C9394A;
        }
        &:last-child {
          margin-left: px2rem(7.5);
        }
        &:active {
          background: $color-blue-transparent;
        }
      }
    }
  }
</style>
