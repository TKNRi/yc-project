<template>
  <div class="container">
    <div class="header">
      <ul class="main-header">
        <!-- ...（YC地図システムロゴ） -->
        <li class="header-button-list">
          <p class="">YC地図システム</p>
        </li>
        <!-- 住所検索タブ -->
        <li class="header-button-list" v-for="(tab, key) in tabs" :key="key">
          <BasicTabs
            :text="tab.text"
            borderRadius="0px"
            padding="17px 40px"
            @click="clickTab(tab.value)"
          />
        </li>
      </ul>
      <div>
        <p>{{ userName }}</p>
      </div>

      <!-- 以下はorganismsでまとめるべき
      (例)
      organisms/YCMaps/AddressModal.vue
      organisms/YCMaps/PrintModal.vue
      organisms/YCMaps/UserModal.vue
      organisms/YCMaps/UserAdditionalModal.vue
      organisms/YCMaps/AreaModal.vue
      organisms/YCMaps/AreaAdditionalModal.vue
     -->
      <!-- そうすれば、 -->
      <!-- <AddressModal v-show="is~~" />
      <PrintModal v-show="is~~" />
      <UserModal v-show="is~~" />
      <UserAdditionalModal v-show="is~~" />
      <AreaModal v-show="is~~" />
      <AreaAdditionalModal v-show="is~~" /> -->
      <!-- の記述だけでいけますよ -->

      <!-- 住所モーダル -->
      <BasicModal v-show="isAddressModal" title="住所検索">
        <template #content>
          <!-- 住所検索モーダルの内容 -->
          <div class="modal-content">
            <div class="modal-content-section">
              <label><input type="radio" name="radio" /></label>
              <BasicInput
                label="住所をあいまい検索"
                type="text"
                name="name"
                placeholder="住所を入力してください。"
                width="50vw;"
                height="30px"
                marginRight="30px"
              />
            </div>
            <div class="modal-content-section">
              <label><input type="radio" name="radio" /></label>
              <BasicInput
                label="住所を郵便番号で検索"
                type="text"
                name="name"
                placeholder="000-0000"
                width="10vw"
                height="30px"
                marginRight="14px"
              />
            </div>
            <div class="modal-content-section">
              <label><input type="radio" name="radio" />住所を選択</label>
              <div class="modal-content-select">
                <BasicSelect
                  v-model="selectedValue"
                  {{
                  selectedValue
                  }}
                  label="都道府県"
                  type="text"
                  name="name"
                  width="5vw"
                  height="10hw"
                  marginRight="6px"
                />
                <BasicSelect
                  label="市区町村"
                  type="text"
                  name="name"
                  width="5vw"
                  height="10hw"
                  marginRight="6px"
                />
                <BasicSelect
                  label="大字"
                  type="text"
                  name="name"
                  width="5vw"
                  height="10hw"
                  marginRight="6px"
                />
                <BasicSelect
                  label="字丁目"
                  type="text"
                  name="name"
                  width="5vw"
                  height="10hw"
                  marginRight="6px"
                />
                <BasicSelect
                  label="街/区"
                  type="text"
                  name="name"
                  width="5vw"
                  height="10hw"
                  marginRight="6px"
                />
                <BasicSelect
                  label="地番/戸番"
                  type="text"
                  name="name"
                  width="5vw"
                  height="10hw"
                  marginRight="6px"
                />
              </div>
              <!--<template #wrapper></template>
                    </BasicSelect>-->
            </div>
            <div class="modal-btn">
              <BasicButton
                text="閉じる"
                color="#fff"
                backGround="#808080"
                borderRadius="0px"
                padding="8px 30px"
                @click="closeAddressModal"
              />
              <BasicButton
                text="検索"
                color="#fff"
                backGround="#008000"
                borderRadius="0px"
                padding="8px 30px"
              />
            </div>
          </div>
        </template>
      </BasicModal>

      <!-- 印刷モーダル -->
      <BasicModal v-show="isPrintingModal" title="印刷設定">
        <template #content>
          <!-- 印刷設定モーダルの内容 -->
        </template>
      </BasicModal>
      <!--<BasicModalUser v-show="isPrintingModal"
            title="ユーザー">
            <template #content>
              <div class="modal-content">
                  <BasicInputUser
                    label="ログインID"
                    width="80%"
                    height="30px"
                    placeholder="半角英数20字以内で入力してください"
                    type="text"
                  />
                  <BasicInputUser
                    label="パスワード"
                    width="80%"
                    height="30px"
                    placeholder="半角英数20字以内で入力してください"
                    type="password"
                  />
                  <BasicInputUser
                    label="パスワード確認"
                    width="80%"
                    height="30px"
                    placeholder="確認のため、パスワードを再度入力してください"
                    type="password"
                  />
                  <BasicInputUser
                    label="ユーザー名"
                    width="80%"
                    height="30px"
                    placeholder="20字以内で入力してください"
                    type="text"
                  />
                  <BasicSelectUser
                    label="権限"
                    width="80%"
                    height="30px"
                  />
                  <BasicSelectUser
                    label="本社"
                    width="80%"
                    height="30px"
                  />
                  <BasicSelectUser
                    label="エリア"
                    width="80%"
                    height="30px"
                  />
                  <div class="modal-btn">
                    <BasicButton
                      text="キャンセル"
                      color="#fff"
                      backGround="#808080"
                      borderRadius="0px"
                      padding="8px 30px"
                      @click="closeAddressModal"
                    />
                    <BasicButton
                      text="削除"
                      color="#fff"
                      backGround="#FF0000"
                      borderRadius="0px"
                      padding="8px 30px"
                    />
                    <BasicButton
                      text="登録"
                      color="#fff"
                      backGround="#008000"
                      borderRadius="0px"
                      padding="8px 30px"
                    />
                  </div>
              </div>
            </template>
          </BasicModalUser>-->

      <!-- ユーザーモーダル -->
      <BasicModal v-show="isUserManagementModal" title="ユーザー管理">
        <template #content>
          <!-- ユーザー管理モーダルの内容 -->
          <div class="modal-content">
            <table>
              <tr>
                <th>操作</th>
                <th>ログインID</th>
                <th>ユーザー名</th>
                <th>権限</th>
                <th>エリア</th>
                <th>更新日時</th>
              </tr>
              <tr>
                <td>編集</td>
                <td>kanri</td>
                <td>管理一郎</td>
                <td>管理権限</td>
                <td>全国</td>
                <td>2022/01/01 00:00:00</td>
              </tr>
              <tr>
                <td>編集</td>
                <td>hensyu</td>
                <td>編集二郎</td>
                <td>編集権限</td>
                <td>東京</td>
                <td>2022/01/01 00:00:00</td>
              </tr>
              <tr>
                <td>編集</td>
                <td>etsuran</td>
                <td>閲覧三郎</td>
                <td>閲覧権限</td>
                <td>大阪</td>
                <td>2022/01/01 00:00:00</td>
              </tr>
            </table>
            <div class="modal-btn">
              <BasicButton
                text="閉じる"
                color="#fff"
                backGround="#808080"
                borderRadius="0px"
                padding="8px 30px"
                @click="closeAddressModal"
              />
              <BasicButton
                text="ユーザー追加"
                color="#fff"
                backGround="#008000"
                borderRadius="0px"
                padding="8px 30px"
                @click="openRegistrationUserModal"
              />

              <!--<BasicModal v-show="isAddUserModalOpen"
                    title="ユーザー">
                      <template #content>
                        <div class="modal-content">
                          <div class="modal-btn">
                            <div class="modal-btn">
                              <BasicButton
                                text="キャンセル"
                                color="#fff"
                                backGround="#808080"
                                borderRadius="0px"
                                padding="8px 30px"
                                @click="closeAddressModal"
                              />
                              <BasicButton
                                text="削除"
                                color="#fff"
                                backGround="#FF0000"
                                borderRadius="0px"
                                padding="8px 30px"
                                @click="closeAddressModal"
                              />
                              <BasicButton
                                text="登録"
                                color="#fff"
                                backGround="#008000"
                                borderRadius="0px"
                                padding="8px 30px"
                              />
                            </div>
                          </div>
                        </div>
                      </template>
                    </BasicModal>-->
            </div>
          </div>
        </template>
      </BasicModal>
      <BasicModalUser v-show="isRegistrationUserModalOpen" title="ユーザー">
        <template #content>
          <!-- ユーザーの内容 -->
          <div class="modal-content">
            <BasicInputUser
              label="ログインID"
              width="80%"
              height="30px"
              placeholder="半角英数20字以内で入力してください"
              type="text"
            />
            <BasicInputUser
              label="パスワード"
              width="80%"
              height="30px"
              placeholder="半角英数20字以内で入力してください"
              type="password"
            />
            <BasicInputUser
              label="パスワード確認"
              width="80%"
              height="30px"
              placeholder="確認のため、パスワードを再度入力してください"
              type="password"
            />
            <BasicInputUser
              label="ユーザー名"
              width="80%"
              height="30px"
              placeholder="20字以内で入力してください"
              type="text"
            />
            <BasicSelectUser label="権限" width="80%" height="30px" />
            <BasicSelectUser label="本社" width="80%" height="30px" />
            <BasicSelectUser label="エリア" width="80%" height="30px" />
            <div class="modal-btn">
              <BasicButton
                text="キャンセル"
                color="#fff"
                backGround="#808080"
                borderRadius="0px"
                padding="8px 30px"
                @click="closeRegistrationUserModal"
              />
              <BasicButton
                text="削除"
                color="#fff"
                backGround="#FF0000"
                borderRadius="0px"
                padding="8px 30px"
              />
              <BasicButton
                text="登録"
                color="#fff"
                backGround="#008000"
                borderRadius="0px"
                padding="8px 30px"
              />
            </div>
          </div>
        </template>
      </BasicModalUser>

      <!-- エリアモーダル -->
      <BasicModal v-show="isAreaManagementModal" title="エリア管理">
        <template #content>
          <!-- エリア管理モーダルの内容 -->
          <div class="modal-content">
            <table>
              <tr>
                <th>操作</th>
                <th>エリアコード</th>
                <th>エリア</th>
                <th>更新日時</th>
              </tr>
              <tr>
                <td>編集</td>
                <td>01</td>
                <td>全国</td>
                <td>2022/01/01 00:00:00</td>
              </tr>
              <tr>
                <td>編集</td>
                <td>02</td>
                <td>東京</td>
                <td>2022/01/01 00:00:00</td>
              </tr>
              <tr>
                <td>編集</td>
                <td>03</td>
                <td>大阪</td>
                <td>2022/01/01 00:00:00</td>
              </tr>
            </table>
            <div class="modal-btn">
              <BasicButton
                text="閉じる"
                color="#fff"
                backGround="#808080"
                borderRadius="0px"
                padding="8px 30px"
                @click="closeAddressModal"
              />
              <BasicButton
                text="エリア追加"
                color="#fff"
                backGround="#008000"
                borderRadius="0px"
                padding="8px 30px"
              />
            </div>
          </div>
        </template>
      </BasicModal>

      <div class="accordion-box">
        <div class="accordion">
          <BasicAccordion />
        </div>
      </div>
    </div>

    <div class="main">
      <div class="footer">
        <FooterAccordion />
      </div>
    </div>
  </div>
</template>

<script setup>
import { BasicButton } from "@/components/atoms/Buttons";
import { BasicInput, BasicInputUser } from "@/components/atoms/Inputs";
import { BasicSelect, BasicSelectUser } from "@/components/atoms/Selects";
import { BasicTabs } from "@/components/atoms/Tabs";
import { BasicModal, BasicModalUser } from "@/components/atoms/Modals";
import { BasicAccordion, FooterAccordion } from "@/components/atoms/Accordions";

// 初期モーダルの表示状態
const isAddressModal = ref(false);
const isPrintingModal = ref(false);
const isUserManagementModal = ref(false);
const isAreaManagementModal = ref(false);
const isRegistrationUserModalOpen = ref(false);

const tabs = reactive([
  { text: "住所検索", value: "address" },
  { text: "印刷設定", value: "print" },
  { text: "ユーザー管理", value: "user" },
  { text: "エリア管理", value: "area" },
]);

const clickTab = (value) => {
  if (value === "address") isAddressModal.value = !isAddressModal.value;
  else if (value === "print") isPrintingModal.value = !isPrintingModal.value;
  else if (value === "user")
    isUserManagementModal.value = !isUserManagementModal.value;
  else if (value === "area")
    isAreaManagementModal.value = !isAreaManagementModal.value;
};

//モーダルの閉じるボタン押下時、モーダル閉じる
const closeAddressModal = () => {
  isUserManagementModal.value = false;
  isAreaManagementModal.value = false;
  isAddressModal.value = false;
  isPrintingModal.value = false;
};

const openRegistrationUserModal = () => {
  isRegistrationUserModalOpen.value = true;
  // isUserManagementModal.value = false;
};

// 選択された値を保持する変数
const selectedValue = ref("");

//ユーザー名をuserNameに表示
const userName = ref("");

//ユーザー追加画面を閉じる
const closeRegistrationUserModal = () => {
  isRegistrationUserModalOpen.value = false;
};

const closeModal = () => {
  isUserManagementModal.value = false;
  isAreaManagementModal.value = false;
  // isRegistrationUserModalOpen.value = false;
};

const openModal = closeModal();
</script>

<style lang="scss" scoped>
.container {
  height: 800px;
  min-height: 100vh; /* ←コンテンツの高さの最小値＝ブラウザの高さに指定 */
  position: relative; /* ←相対位置 */
  //padding-bottom: 60px; /* ←フッターの高さを指定 */
  box-sizing: border-box;
  /* ↑ヘッダーやフッターを含むすべての要素の高さ＝min-height:100vhになるように指定 */
  border: solid 1px #000;
}

.main {
}

.header {
  display: flex;
  justify-content: space-between;
  position: relative;
  border-bottom: solid 1px #000;
}

.main-header {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.header-img {
}

.header-button-list {
  //border: solid 0.5px #000;
}

.header-button {
  padding: 16px 40px;
  border: solid 1px #000;
  cursor: pointer;
}

.accordion-open {
  background-color: #fff;
}

.accordion-button {
  width: 20px;
  cursor: pointer;
  position: absolute;
  margin: auto;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  margin-right: 100px;
}

.footer {
  position: absolute; /* ←絶対位置 */
  bottom: 0;
  width: 100%;

  /* 以下 背景色やテキストカラーなどはお好みで指定してください */
  //background: #fff;
  color: #fff;
  border-top: solid 1px #000;
}

table {
  width: 95%;
  border-collapse: separate;
  border-spacing: 0;
  margin: 0 auto;
  margin-top: 10px;
}

table th:first-child {
  border-radius: 5px 0 0 0;
}

table th:last-child {
  border-radius: 0 5px 0 0;
  border-right: 1px solid #3c6690;
}

table th {
  text-align: center;
  color: white;
  background: linear-gradient(#829ebc, #225588);
  border-left: 1px solid #3c6690;
  border-top: 1px solid #3c6690;
  border-bottom: 1px solid #3c6690;
  box-shadow: 0px 1px 1px rgba(255, 255, 255, 0.3) inset;
}

table td {
  text-align: center;
  border-left: 1px solid #a8b7c5;
  border-bottom: 1px solid #a8b7c5;
  border-top: none;
  box-shadow: 0px -3px 5px 1px #eee inset;
  width: 12%;
  padding: 10px 0;
}

table td:last-child {
  border-right: 1px solid #a8b7c5;
}

table tr:last-child td:first-child {
  border-radius: 0 0 0 5px;
}

.modal-content {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: block;
  width: 95%;
  z-index: 100;
}

.modal-content-section {
  display: flex;
  align-items: center;
  gap: 5px;
  margin-top: 30px;
}

.modal-content-select {
  display: flex;
  //align-items: center;
  gap: 20px;
  margin-top: 30px;
}
</style>

<style lang="scss" scoped>
.modal-btn {
  display: flex;
  float: right;
  position: relative;
  right: 20px;
  gap: 20px;
  bottom: -80px;
}

.modal-default-button {
  float: right;
}
</style>
