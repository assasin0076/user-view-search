<script setup>
  import { onBeforeMount, ref } from 'vue';
  import throttle from '@/helpers/throttle';

  const users = ref([]);
  const filteredUsers = ref([]);
  const selectedUser = ref();
  const searchValue = ref('');

  const selectUser = (id) => {
    selectedUser.value = users.value.find((user) => user.id === id);
  };

  const searchUsers = throttle(() => {
    selectedUser.value = null;
    const parts = searchValue.value
      .split(',')
      .filter((part) => String(part).length > 0)
      .map((part) => {
        if (!part.length) return part;
        return isNaN(part) ? part : parseInt(part);
      })
      .reduce((acc, part) => {
        if (typeof part === 'string') {
          return [...acc, { type: 'name', value: part }];
        }
        if (typeof part === 'number') {
          return [...acc, { type: 'id', value: part }];
        }
      }, []);
    if (!parts.length) {
      filteredUsers.value = users.value;
      return;
    }
    filteredUsers.value = users.value.filter((user) => {
      return parts.some((part) => {
        if (part.type === 'id') {
          return user.id === part.value;
        } else {
          return user.name === part.value;
        }
      });
    });
  }, 200);

  onBeforeMount(async () => {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    const json = await response.json();
    users.value = json;
    filteredUsers.value = json;
  });
</script>

<template>
  <div class="main-page">
    <header class="header-block">
      <img alt="Vue logo" class="logo" src="./assets/logo.svg" />
    </header>

    <main class="content-block">
      <div class="search-section">
        <h2 class="header-text mb-14">Поиск сотрудников</h2>
        <input
          v-model="searchValue"
          class="search-input"
          placeholder="Antonette, Bret"
          @input="searchUsers"
        />
        <h2 class="header-text">Результаты</h2>
        <div v-if="users.length === 0" class="thin-text mt-10">
          ничего не найдено
        </div>
        <div class="results-container" v-else>
          <div
            v-for="user in filteredUsers"
            :key="user.id"
            class="result-item"
            :class="{ 'result-item__selected': user.id === selectedUser?.id }"
            @click="selectUser(user.id)"
          >
            <img
              class="result-image"
              src="./assets/image-stub-small.jpg"
              alt="#"
            />
            <div class="result-item-description">
              <div class="bold-text result-item-name">{{ user.name }}</div>
              <div class="thin-text result-item-email">{{ user.email }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="profile-section" v-if="selectedUser">
        <img
          class="profile-section-image"
          src="./assets/image-stub-big.jpg"
          alt="#"
        />
        <div class="profile-section-stats">
          <div class="header-text mb-10">{{ selectedUser.name }}</div>
          <div class="stat-group mb-10">
            <div class="bold-text">email:</div>
            <div class="designer-dolboyob">&nbsp;&nbsp;</div>
            <div class="thin-text">{{ selectedUser.email }}</div>
          </div>
          <div class="stat-group mb-20">
            <div class="bold-text">phone:</div>
            <div class="designer-dolboyob">&nbsp;&nbsp;</div>
            <div class="thin-text">{{ selectedUser.phone }}</div>
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
      <div class="profile-section-empty-stub" v-else>
        Выберите сотрудника, чтобы посмотреть его профиль
      </div>
    </main>
  </div>
</template>

<style scoped lang="scss">
  .main-page {
    padding: 50px;
    height: 100vh;
    max-height: 100vh;
    display: flex;
    flex-direction: column;

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
    .mt-10 {
      margin-top: 10px;
    }

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
      height: auto;
      background-color: var(--main-bg);
      filter: drop-shadow(0px 0px 10px rgba(0, 0, 0, 0.1));
      border-radius: 10px;
      display: grid;
      grid-template-columns: 290px auto;
      flex-grow: 1;
      max-height: 100%;
      overflow: hidden;

      .search-section {
        padding: 24px 20px;
        border-right: 1px solid var(--main-border);
        display: flex;
        flex-direction: column;
        flex: 1;
        overflow: hidden;

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

        .results-container {
          flex: 1;
          overflow: hidden;
          overflow-y: auto;
          max-height: 100%;
          display: flex;
          flex-direction: column;
          &::-webkit-scrollbar {
            width: 26px;
            border-radius: 13px;
            background-clip: padding-box;
            border: 10px solid transparent;
          }
          &::-webkit-scrollbar-track {
            background-color: transparent;
          }
          &::-webkit-scrollbar-thumb {
            width: 26px;
            border-radius: 13px;
            background-clip: padding-box;
            border: 10px solid transparent;
            color: var(--main-border);
          }
          &::-webkit-scrollbar-thumb {
            box-shadow: inset 0 0 0 10px;
          }
          .result-item {
            display: flex;
            border-radius: 10px;
            box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.1);
            cursor: pointer;
            border: 1px solid transparent;
            transition:
              border 0.2s,
              background-color 0.2s;

            &:hover {
              background-color: var(--main-border);
            }

            &:not(:last-child) {
              margin-bottom: 18px;
            }

            &:first-child {
              margin-top: 18px;
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
              overflow: hidden;

              .result-item-name {
                text-overflow: ellipsis;
                overflow: hidden;
                white-space: nowrap;
                margin-bottom: 5px;
              }
              .result-item-email {
                text-overflow: ellipsis;
                overflow: hidden;
                white-space: nowrap;
              }
            }

            &.result-item__selected {
              border: 1px solid var(--main-border);
              cursor: default;
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
