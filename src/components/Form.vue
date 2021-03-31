<template>
  <form class="sign-up" action="" @submit.prevent="onSubmit()">
    <div class="general">
      <section class="sign-form">
        <h2 class="general__title">Заполните форму</h2>
        <p class="general__description">
          <span class="star"><img src="../assets/bull.png" alt="" /></span> -
          поля обязательные для заполнения
        </p>
        <div class="sign-form__form-group">
          <label
            ><span class="star"><img src="../assets/bull.png" alt="" /></span
            >Фамилия
          </label>
          <input
            type="text"
            class="sign-form__surname"
            :class="$v.form.surname.$error ? 'error2' : ''"
            v-model.trim="form.surname"
          />
          <p
            v-if="$v.form.surname.$dirty && !$v.form.surname.required"
            class="error"
          >
            Обязательное поле
          </p>
        </div>
        <div class="sign-form__form-group">
          <label
            ><span class="star"><img src="../assets/bull.png" alt="" /></span
            >Имя
          </label>
          <input
            class="sign-form__name"
            type="text"
            :class="$v.form.name.$error ? 'error2' : ''"
            v-model.trim="form.name"
          />
          <p v-if="$v.form.name.$dirty && !$v.form.name.required" class="error">
            Обязательное поле
          </p>
        </div>
        <div class="sign-form__form-group">
          <label class="test">Отчество</label>
          <input
            type="text"
            class="sign-form__patronymic"
            v-model.trim="form.patronymic"
          />
        </div>
        <div class="sign-form__numbers">
          <div class="sign-form__form-group">
            <label
              ><span class="star"><img src="../assets/bull.png" alt="" /></span>
              Дата рождения
            </label>
            <input
              class="sign-form__date"
              type="date"
              name="date"
              :class="$v.form.date.$error ? 'error2' : ''"
              v-model.trim="form.date"
            />
            <p
              v-if="$v.form.date.$dirty && !$v.form.date.required"
              class="error"
            >
              Обязательное поле
            </p>
          </div>
          <div class="sign-form__form-group">
            <label
              ><span class="star"><img src="../assets/bull.png" alt="" /></span
              >Телефон
            </label>
            <input
              type="tel"
              class="sign-form__phone"
              v-model.trim="form.tel"
              name="phone"
              id="phone"
              placeholder="7-000-00-00"
              autocomplete="tel"
              v-phone
              :class="$v.form.tel.$error ? 'error2' : ''"
            />
            <p v-if="$v.form.tel.$dirty && !$v.form.tel.required" class="error">
              Обязательное поле
            </p>
            <p
              v-if="$v.form.tel.$dirty && !$v.form.tel.minLength"
              class="error"
            >
              Ровно 11 символов
            </p>
          </div>
        </div>
        <div class="sign-form__gender">
          <div class="sign-form__form-group">
            <label>
              <input type="radio" value="male" v-model="form.gendere" />
              Мужчина
            </label>
          </div>
          <div class="sign-form__form-group">
            <label>
              <input type="radio" value="female" v-model="form.gendere" />
              Женщина
            </label>
          </div>
        </div>
        <div class="sign-form__form-group group__clients">
          <label
            ><span class="star"><img src="../assets/bull.png" alt="" /></span>
            Группа клиентов
            <p
              :class="$v.form.SelectedClients.$error ? 'error4' : ''"
              class="group__clients--description"
            >
              (при необходимости выберите несколько пунктов)
            </p>
            <p v-if="$v.form.tel.$dirty && !$v.form.tel.required" class="error">
              Обязательное поле
            </p></label
          >

          <select
            class="sign-form__select-clients multselect"
            v-model="form.SelectedClients"
            :class="$v.form.SelectedClients.$error ? 'error3' : ''"
            multiple
          >
            <option
              v-for="(GroupClient, index) in GroupClients"
              :value="GroupClient.value"
              :key="index"
            >
              {{ GroupClient.text }}
            </option>
          </select>
        </div>
        <div class="sign-form__doctors-wrapper">
          <div class="sign-form__form-group">
            <label>Лечащий врач</label>
            <select v-model="form.WhoMyDoc" class="sign-form__select-doctors">
              <option
                v-for="(doc, index) in docs"
                :value="doc.value"
                :key="index"
              >
                {{ doc.text }}
              </option>
            </select>
          </div>

          <div class="sign-form__form-group checkbox">
            <label class="checkbox__label">
              Не отправлять смс?
              <input
                type="checkbox"
                class="checkbox__input"
                v-model="form.checked"
              />
              <span class="checkbox__span"></span>
            </label>
          </div>
        </div>
      </section>
      <section class="adress">
        <h2>Адрес</h2>
        <div class="adress__form-group">
          <label class="test">Индекс</label>
          <input
            type="number"
            class="adress__post-index"
            v-model.trim="form.PostIndex"
          />
        </div>
        <div class="adress__form-group">
          <label class="test">Страна</label>
          <input
            type="text"
            class="adress__country"
            v-model.trim="form.country"
          />
        </div>
        <div class="adress__form-group">
          <label class="test">Область</label>
          <input
            type="text"
            class="adress__region"
            v-model.trim="form.region"
          />
        </div>
        <div class="adress__form-group">
          <label
            ><span class="star"><img src="../assets/bull.png" alt="" /></span>
            Город
          </label>
          <input
            type="text"
            class="adress__region"
            v-model.trim="form.city"
            :class="$v.form.city.$error ? 'error2' : ''"
          />
          <p v-if="$v.form.city.$dirty && !$v.form.city.required" class="error">
            Обязательное поле
          </p>
        </div>
        <div class="adress__form-group">
          <label class="test">Улица</label>
          <input
            type="text"
            class="adress__street"
            v-model.trim="form.street"
          />
        </div>
        <div class="adress__form-group">
          <label class="test">Дом</label>
          <input
            type="text"
            class="adress__home-number"
            v-model.trim="form.HomeNumber"
          />
        </div>
      </section>
      <section class="passport">
        <h2>Документ</h2>
        <div class="passport__group">
          <div class="passport__form-group">
            <label
              ><span class="star-two"
                ><img src="../assets/bull.png" alt="" /></span
              >Тип документа
            </label>
            <select
              :class="$v.form.TypeDocument.$error ? 'error2' : ''"
              v-model="form.TypeDocument"
              class="passport__type-document"
            >
              <option
                v-for="(document, index) in documents"
                :value="document.value"
                :key="index"
              >
                {{ document.text }}
              </option>
            </select>
            <p
              v-if="
                $v.form.TypeDocument.$dirty && !$v.form.TypeDocument.required
              "
              class="error"
            >
              Обязательное поле
            </p>
          </div>
          <div class="passport__form-group">
            <label
              ><span class="star-two"
                ><img src="../assets/bull.png" alt="" /></span
              >Дата выдачи</label
            >
            <input
              type="date"
              id="date"
              class="passport__when-gave"
              :class="$v.form.WhenGave.$error ? 'error2' : ''"
              v-model.trim="form.WhenGave"
            />
            <p
              v-if="$v.form.WhenGave.$dirty && !$v.form.WhenGave.required"
              class="error"
            >
              Обязательное поле
            </p>
          </div>
        </div>
        <div class="passport__form-group">
          <label class="test">Серия</label>
          <input
            type="number"
            class="passport__series"
            v-model.trim="form.series"
          />
        </div>
        <div class="passport__form-group">
          <label class="test">Номер</label>
          <input
            type="number"
            class="passport__passport-number"
            v-model.trim="form.PasportNumbers"
          />
        </div>
        <div class="passport__form-group">
          <label class="test">Кем выдан</label>
          <textarea
            type="text"
            class="passport__who-give"
            v-model.trim="form.WhoGive"
          ></textarea>
        </div>
      </section>
      <input class="general__submit" type="submit" value="Отправить" />
    </div>
    <modal v-show="isModalVisible" @close="closeModal" />
  </form>
</template>

<script>
import { required, minLength } from "vuelidate/lib/validators";
import modal from "@/components/Modal";

export default {
  data() {
    return {
      form: {
        surname: [],
        name: [],
        date: [],
        tel: [],
        SelectedClients: [],
        checked: false,
        gendere: "male",
        patronymic: [],
        WhoMyDoc: "ivanov",

        PostIndex: [],
        country: [],
        region: [],
        city: [],
        street: [],
        HomeNumber: [],

        TypeDocument: "passport",
        series: [],
        PasportNumbers: [],
        WhoGive: [],
        WhenGave: [],
      },
      isModalVisible: false,
      GroupClients: [
        { text: "VIP", value: "vip" },
        { text: "Проблемные", value: "problem" },
        { text: "ОМС", value: "free" },
      ],
      docs: [
        { text: "Иванов", value: "ivanov" },
        { text: "Захаров", value: "zakharov" },
        { text: "Чернышева", value: "chernicheva" },
      ],
      documents: [
        { text: "Паспорт", value: "passport" },
        { text: "Свидетельство о рождении", value: "witnessto" },
        { text: "Вод. удостоверение", value: "drivers" },
      ],
    };
  },
  validations: {
    form: {
      surname: { required },
      name: { required },
      date: { required },
      tel: { required, minLength: minLength(14) },
      SelectedClients: { required },
      city: { required },
      TypeDocument: { required },
      WhenGave: { required },
    },
  },
  methods: {
    onSubmit() {
      this.$v.form.$touch();
      if (!this.$v.form.$error) {
        this.isModalVisible = true;
      }
    },
    closeModal() {
      this.isModalVisible = false;
    },
  },
  components: {
    modal,
  },
};
</script>

<style scoped lang="scss">
//<глобально>===========================================================================================================

input[type="text"] {
  background-color: rgba(131, 152, 184, 0.3);
  border-radius: 50px;
  padding: 18px 25px;
  width: 100%;
  color: #fff;
  font-style: normal;
  font-weight: bold;
  font-size: 23px;
  line-height: 19px;
  &:focus {
    border: 1px solid #ffffff;
  }
}

input[type="number"] {
  background-color: rgba(131, 152, 184, 0.3);
  border-radius: 50px;
  padding: 18px 25px;
  width: 100%;
  font-style: normal;
  font-weight: bold;
  font-size: 23px;
  line-height: 19px;

  color: #ffffff;
  &:focus {
    border: 1px solid #ffffff;
  }
}

input[type="date"] {
  background-color: rgba(131, 152, 184, 0.3);
  border-radius: 50px;
  padding: 13px 19px;
  width: 100%;
  height: 70px;
  text-transform: uppercase;

  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  line-height: 19px;

  color: #c5d0e0;
  &:focus {
    border: 1px solid #ffffff;
  }
}

input[type="tel"] {
  background-color: rgba(131, 152, 184, 0.3);
  border-radius: 50px;
  padding: 13px 19px;
  width: 100%;
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  line-height: 19px;
  height: 70px;
  color: #ffffff;
  &:focus {
    border: 1px solid #ffffff;
  }
}

input[type="tel"]::placeholder {
  color: #c5d0e0;
}

label {
  display: block;
  text-align: left;
  padding: 0px 0px 10px 5px;
  font-weight: 600;
}

select {
  display: block;
  background-color: rgba(131, 152, 184, 0.3);
  text-align: center;
  border-radius: 34px;

  font-size: 18px;
  font-weight: 700;
  color: #000;
  padding: 13px 19px;
  max-width: 100%;
  box-sizing: border-box;
  margin: 0;
  box-shadow: 0 1px 0 1px rgba(0, 0, 0, 0.04);
  appearance: none;
  background-repeat: no-repeat, repeat;
  background-position: right 0.7em top 50%, 0 0;
  background-size: 0.65em auto, 100%;
}
.select-css::-ms-expand {
  display: none;
}
.select-css:hover {
  border-color: #888;
}
.select-css:focus {
  border-color: #aaa;
  box-shadow: 0 0 1px 3px #fff;
  box-shadow: 0 0 0 3px;
  color: #222;
  outline: none;
}

//<Основное>===========================================================================================================

.error {
  font-style: italic;
  font-weight: 300;
  font-size: 16px;
  line-height: 25px;
  padding: 0px 0px 0px 35px;
  background: url("../assets/err.svg") 10px 5px no-repeat;
  text-align: left;
  color: #fff;
}

.error2 {
  border: 1px solid red;
}

.error3 {
  border: 2px solid red;
}

.error4 {
  color: red;
}

.sign-up {
}
.general {
  text-align: center;
  padding: 0px 0px 40px 0px;

  &__title {
    font-style: normal;
    font-weight: bold;
    font-size: 32px;
    line-height: 30px;
    text-align: center;
    line-height: 38px;

    color: #ffffff;

    padding: 50px 0px 25px 0px;
    text-transform: uppercase;
  }

  &__submit {
    background: #22b2ea;
    border-radius: 55px;
    font-style: normal;
    font-weight: 500;
    font-size: 18px;
    line-height: 17px;
    padding: 18px 75px;
    color: #ffffff;
    cursor: pointer;

    &:hover {
      background: #1bbfff;
      border: 0.5px solid #9ae3ff;
      box-sizing: border-box;
      box-shadow: 0px 0px 7px #4ab1d9, 0px 0px 16px #00b8ff;
    }
    font-size: 18px;
  }

  &__description {
    text-align: center;
    padding: 0px 0px 25px 0px;

    font-style: italic;
    font-weight: 300;
    font-size: 16px;
    line-height: 18px;
    max-width: 250px;
    margin: 0px auto;
  }
}
.sign-form {
  &__numbers {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }

  &__form-group {
    padding: 10px 0px 10px 0px;
    font-family: Rubik;
    font-style: normal;
    font-weight: normal;
    font-size: 19px;
    line-height: 14px;
    text-align: center;

    color: #c5d0e0;
    span {
      padding: 0px 10px 0px 0px;
    }
  }

  &__date {
    text-align: center;
    max-width: 220px;
    letter-spacing: 1.5px;
    display: flex;
    font-size: 16px;
    height: 50px;
  }

  &__phone {
    max-width: 190px;
    display: flex;
    overflow: hidden;
    letter-spacing: 1.5px;
    font-size: 18px;
    padding: 0px 0px;
    height: 50px;
  }

  &__gender {
    padding: 35px 0px;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    input {
      margin: 0px 10px 0px 0px;
    }
  }
  &__select-clients {
    overflow: hidden;
    align-items: center;
  }

  &__doctors-wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
  }

  &__select-doctors {
    background-image: url("data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%23007CB2%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%2Fsvg%3E"),
      linear-gradient(to bottom, #fff 0%, #fff 100%);
    width: 180px;
    height: 70px;
  }

  &__sms {
  }
}

.adress {
  &__form-group {
    padding: 10px 0px;
    font-style: normal;
    font-weight: normal;
    font-size: 19px;
    line-height: 14px;
    text-align: center;

    color: #c5d0e0;
  }
}
.passport {
  padding: 0px 0px 30px 0px;
  &__form-group {
    padding: 10px 0px;
    font-style: normal;
    font-weight: normal;
    font-size: 19px;
    line-height: 14px;
    text-align: center;

    color: #c5d0e0;
  }

  &__group {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;

    p {
      max-width: 100px;
    }
  }

  &__type-document {
    background-image: url("data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%23007CB2%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%2Fsvg%3E"),
      linear-gradient(to bottom, #fff 0%, #fff 100%);
    width: 75%;
    height: 70px;
  }

  &__who-give {
    width: 100%;
    height: 130px;
    padding: 5px 25px;

    background-color: rgba(131, 152, 184, 0.3);
    border-radius: 26.2971px;
    width: 100%;

    font-style: normal;
    font-weight: bold;
    font-size: 23px;
    line-height: 19px;

    color: #ffffff;
  }

  &__when-gave {
    max-width: 190px;
    display: flex;
    font-size: 16px;
    height: 50px;

    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 19px;
  }
}

.group__clients {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 0px 0px 15px 0px;
  p {
    margin: 10px 0px 0px 0px;
    padding: 5px 0px 0px 30px;
    max-width: 250px;
    font-style: italic;
    font-weight: 300;
    font-size: 16px;
    line-height: 18px;
  }
}

h2 {
  font-style: normal;
  font-weight: bold;
  font-size: 25px;
  line-height: 30px;
  text-align: center;
  line-height: 38px;

  color: #ffffff;
  text-transform: uppercase;
  padding: 50px 0px 40px 0px;
}

.star {
  img {
    padding: 3.2px 5px 0px 0px;
  }
}

.star-two {
  img {
    padding: 5px 10px 0px 0px;
  }
}

.checkbox {
  padding: 40px 0px 0px 0px;
}
.checkbox__span {
  position: relative;
  margin: 0px 0px 0px 20px;
  width: 20px;
  height: 20px;
  border: 1px solid #ccc;
  background-color: #fff;
  display: inline-block;
  border-radius: 50%;
  transition: all linear 0.3s;
  &:after {
    content: "";
    position: absolute;
    display: block;
    top: 0;
    left: 40%;
    border-bottom: 2px solid blue;
    border-right: 2px solid blue;
    height: 15px;
    width: 7px;
    transform: rotate(45deg);
    visibility: hidden;
  }
}
.checkbox__input {
  display: none;
  &:checked ~ span {
    background: #cccccc;
    &:after {
      visibility: visible;
    }
  }
}

.checkbox__label {
  display: flex;
  align-items: center;
}

.group {
  &__clients--description {
    font-style: italic;
    font-weight: 300;
    font-size: 14px;
    line-height: 12px;
  }
}

.test {
  margin: 0px 0px 0px 20px;
}

.multselect {
  background-color: rgba(131, 152, 184, 0.3);
  font-style: normal;
  line-height: 14px;
  text-align: center;
  max-height: 130px;
  width: 210px;
  option {
    padding: 8px 0px 0px 0px;
    font-weight: 700;
    font-size: 18px;
  }
  color: #c5d0e0;
}
</style>
