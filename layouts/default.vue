<template>
  <div>
    <nuxt />
    <div class="menu">
      <p>
        <nuxt-link to="/"><i class="material-icons">home</i>TOP</nuxt-link>
      </p>
      <p>
        <nuxt-link to="mypage"
          ><i class="material-icons"> book </i>マイカード一覧</nuxt-link
        >
      </p>
      <p>
        <nuxt-link to="shop"
          ><i class="material-icons"> shopping_cart </i
          >カードショップ</nuxt-link
        >
      </p>
    </div>
  </div>
</template>

<style lang="scss">
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  background: #fafafa;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}

.menu {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  line-height: 64px;
  display: flex;
  justify-content: center;
  background: #000;
  color: white;
  box-shadow: 0 0 10px #333;
  a {
    color: inherit;
    text-decoration: none;
    text-align: center;
    display: block;
    transition: 0.3s;
    padding: 0 24px;
    &:hover {
      background: #d52a48;
    }
    .material-icons {
      vertical-align: -5px;
      margin-right: 8px;
    }
  }
}
</style>
