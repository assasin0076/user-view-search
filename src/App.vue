<script setup></script>

<template>
  <div class="main-page">
    <header class="header-block">
      <img alt="Vue logo" class="logo" src="./assets/logo.svg" />
    </header>

    <main class="content-block">
      <div class="search-section">
        <h2 class="header-text mb-14">Поиск сотрудников</h2>
        <input class="search-input" placeholder="Antonette, Bret" />
        <h2 class="header-text mb-18">Результаты</h2>
        <div class="result-item">
          <img
            class="result-image"
            src="./assets/image-stub-small.jpg"
            alt="#"
          />
          <div class="result-item-description">
            <div class="bold-text mb-5">Bret</div>
            <div class="thin-text">Sincere@april.biz</div>
          </div>
        </div>
        <div class="result-item result-item__selected">
          <img
            class="result-image"
            src="./assets/image-stub-small.jpg"
            alt="#"
          />
          <div class="result-item-description">
            <div class="bold-text mb-5">Bret</div>
            <div class="thin-text">Sincere@april.biz</div>
          </div>
        </div>
      </div>
      <div class="profile-section-empty-stub" v-if="false">
        Выберите сотрудника, чтобы посмотреть его профиль
      </div>
      <div class="profile-section" v-else>
        <img
          class="profile-section-image"
          src="./assets/image-stub-big.jpg"
          alt="#"
        />
        <div class="profile-section-stats">
          <div class="header-text mb-10">Ervin Howell</div>
          <div class="stat-group mb-10">
            <div class="bold-text">email:</div>
            <div class="designer-dolboyob">&nbsp;&nbsp;</div>
            <div class="thin-text">Shanna@melissa.tv</div>
          </div>
          <div class="stat-group mb-20">
            <div class="bold-text">phone:</div>
            <div class="designer-dolboyob">&nbsp;&nbsp;</div>
            <div class="thin-text">010-692-6593 x09125</div>
          </div>
          <div class="header-text mb-25">О себе:</div>
          <div class="thin-text">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
            eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim
            ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut
            aliquip ex ea commodo consequat. Duis aute irure dolor in
            reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla
            pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
            culpa qui officia deserunt mollit anim id est laborum.
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<style scoped lang="scss">
  .main-page {
    .mb-5 {
      margin-bottom: 5px;
    }
    .mb-10 {
      margin-bottom: 10px;
    }
    .mb-14 {
      margin-bottom: 14px;
    }
    .mb-18 {
      margin-bottom: 18px;
    }
    .mb-20 {
      margin-bottom: 20px;
    }
    .mb-25 {
      margin-bottom: 25px;
    }
    padding: 50px;

    h2 {
      margin: 0;
    }

    .header-text {
      color: var(--text-bold);
      font-size: 16px;
      font-style: normal;
      font-weight: 600;
      line-height: 140%;
    }
    .bold-text {
      color: var(--text-bold);
      font-size: 14px;
      font-style: normal;
      font-weight: 600;
      line-height: normal;
    }
    .thin-text {
      color: var(--text-thin);
      font-size: 14px;
      font-style: normal;
      font-weight: 400;
      line-height: normal;
    }

    .header-block {
      margin-bottom: 26px;
      .logo {
        padding: 4px;
      }
    }

    .content-block {
      background-color: var(--main-bg);
      filter: drop-shadow(0px 0px 10px rgba(0, 0, 0, 0.1));
      border-radius: 10px;
      display: grid;
      grid-template-columns: 290px auto;

      .search-section {
        padding: 24px 20px;
        border-right: 1px solid var(--main-border);

        .search-input {
          color: #76787d;
          font-size: 14px;
          font-style: normal;
          font-weight: 400;
          line-height: normal;
          padding: 16px 24px;
          outline: none;
          border-radius: 8px;
          border: 1.5px solid var(--main-components);
          background: var(--white);
          margin-bottom: 30px;
        }

        .result-item {
          display: flex;
          border-radius: 10px;
          box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.1);
          cursor: pointer;

          &:not(:last-child) {
            margin-bottom: 18px;
          }

          .result-image {
            border-right: 1px solid var(--main-border);
            border-radius: 10px 0 0 10px;
            width: 70px;
            height: 70px;
          }
          .result-item-description {
            width: 100%;
            padding: 15px;
          }

          &.result-item__selected {
            border: 1px solid var(--main-border);
            cursor: default;
            .result-item-description {
              background-color: var(--main-border);
            }
          }
        }
      }

      .profile-section-empty-stub {
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
      }

      .profile-section {
        padding: 30px 30px 30px 20px;
        display: flex;

        .profile-section-image {
          width: 424px;
          height: 286px;
          margin-right: 60px;
        }

        .profile-section-stats {
          .stat-group {
            display: flex;
          }
        }
      }
    }
  }
</style>
