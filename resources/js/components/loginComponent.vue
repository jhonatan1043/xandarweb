<template>
  <div>
    <div class="form-container outer">
      <div class="form-form">
        <div class="form-form-wrap">
          <div class="form-container">
            <div class="form-content">
              <h1 class="">XANDAR</h1>
              <hr />
              <form class="text-left">
                <div class="form">
                  <div id="username-field" class="field-wrapper input">
                    <label for="username">USUARIO</label>
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      width="24"
                      height="24"
                      viewBox="0 0 24 24"
                      fill="none"
                      stroke="currentColor"
                      stroke-width="2"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      class="feather feather-user"
                    >
                      <path
                        d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"
                      ></path>
                      <circle cx="12" cy="7" r="4"></circle>
                    </svg>
                    <input
                      v-model="username"
                      name="username"
                      type="text"
                      class="form-control"
                      placeholder="xandar"
                    />
                  </div>

                  <div id="password-field" class="field-wrapper input mb-2">
                    <label for="password">PASSWORD</label>
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      width="24"
                      height="24"
                      viewBox="0 0 24 24"
                      fill="none"
                      stroke="currentColor"
                      stroke-width="2"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      class="feather feather-lock"
                    >
                      <rect
                        x="3"
                        y="11"
                        width="18"
                        height="11"
                        rx="2"
                        ry="2"
                      ></rect>
                      <path d="M7 11V7a5 5 0 0 1 10 0v4"></path>
                    </svg>
                    <input
                      v-model="password"
                      name="password"
                      type="password"
                      class="form-control"
                      placeholder="Password"
                    />
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      width="24"
                      height="24"
                      viewBox="0 0 24 24"
                      fill="none"
                      stroke="currentColor"
                      stroke-width="2"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      id="toggle-password"
                      class="feather feather-eye"
                    >
                      <path
                        d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"
                      ></path>
                      <circle cx="12" cy="12" r="3"></circle>
                    </svg>
                  </div>
                  <div class="field-wrapper input mb-2">
                    <label for="idEmpresa">Cliente</label>
                    <select
                      class="form-control"
                      v-model="idBusiness"
                      name="idEmpresa"
                    >
                      <option selected="0" value="0">-- Seleccione --</option>
                      <option
                        v-for="item in arrayEmpresas"
                        :key="item.cod_empresa"
                        :value="item.cod_empresa"
                        v-text="item.nom_empresa"
                      ></option>
                    </select>
                  </div>
                  <div class="d-sm-flex justify-content-between">
                    <div class="field-wrapper">
                      <button
                        type="button"
                        class="btn btn-primary"
                        @click="login()"
                      >
                        Entrar
                      </button>
                    </div>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      arrayEmpresas: [],
      idBusiness: 0,
      username: "",
      password: "",
    };
  },
  methods: {
    businessList() {
      let me = this;
      axios
        .get("api/business/list")
        .then((res) => {
          me.arrayEmpresas = res.data;
        })
        .catch((err) => {
          console.error(err);
        });
    },
    login() {
      let me = this;
      if (me.idBusiness == 0 || me.username == "" || me.password == "") {
        alert("faltan datos");
      } else {
        axios
          .post("api/user/login", {
            username: me.username,
            password: me.password,
            idBusiness: me.idBusiness,
          })
          .then((res) => {
            console.log(res);
            if (res.data.response == 200) {
              window.location.href = "/main";
            } else {
              alert("Credenciales no validas");
            }
          })
          .catch((err) => {
            console.error(err);
          });
      }
    },
  },
  created() {
    this.businessList();
  },
};
</script>
