<template>
  <div id="aut-num-form">
  <form class="vue-form" @submit.prevent="submit">

    <div class="error-message">
      <p v-show="!email.valid">Oh, please enter a valid email address.</p>
      <p v-show="!changed.valid">Oh, please enter a valid email address.</p>
    </div>

    <fieldset>
      <legend>Aut-num form</legend>
      <div>
        <label class="label" for="aut_num">Aut-Num</label>
        <input type="text" name="aut_num" id="aut_num" required="" v-model="aut_num">
      </div>
      <div>
        <label class="label" for="as_name">As-Name</label>
        <input type="text" name="as_name" id="as_name" required="" v-model="as_name">
      </div>
      <div>
        <label class="label" for="textarea">Description</label>
        <textarea class="description" name="textarea" id="textarea" required="" 
                  v-model="description.text" 
                  ></textarea>
      </div>
      <div>
        <h4>Status</h4>
        <p class="select">
          <select class="budget" v-model="selection.status">
						<option value="AFPUB-2004-ASN-001">ASSIGNED</option>
						<option value="AFPUB-2012-V4-001">ASSIGNED-ANYCAST</option>
						<option value="AFPUB-2014-GEN-004">POLICY-RESERVED</option>
					</select>
        </p>
      </div>
      <div>
        <label class="label" for="member_of">Member-of</label>
        <input type="text" name="member_of" id="member_of" v-model="member_of">
      </div>
      <div>
        <label class="label" for="import">Import</label>
        <input type="text" name="import" id="import" v-model="import_policy">
      </div>
      <div>
        <label class="label" for="mp_import">Multiprotocol Import</label>
        <input type="text" name="mp_import" id="mp_import" v-model="mp_import">
      </div>
      <div>
        <label class="label" for="export">Export</label>
        <input type="text" name="export" id="export" v-model="export_policy">
      </div>
      <div>
        <label class="label" for="mp_export">Multiprotocol export</label>
        <input type="text" name="mp_export" id="mp_export" v-model="mp_export">
      </div>
      <div>
        <label class="label" for="default">Default</label>
        <input type="text" name="default" id="default" v-model="default_policy">
      </div>
      <div>
        <label class="label" for="mp_default">Multiprotocol Default</label>
        <input type="text" name="mp_default" id="mp_default" v-model="mp_default">
      </div>
      <div>
        <label class="label" for="textarea">Remarks</label>
        <textarea class="description" name="textarea" id="textarea"
                  v-model="remarks" 
                  ></textarea>
      </div>
      <div>
        <label class="label" for="org">Organisation</label>
        <input type="text" name="org" id="org" required="" v-model="org">
      </div>
      <div>
        <label class="label" for="admin_c">Administrative contact</label>
        <input type="text" name="admin_c" id="admin_c" required="" v-model="admin_c">
      </div>
      <div>
        <label class="label" for="tech_c">Technical contact</label>
        <input type="text" name="tech_c" id="tech_c" required="" v-model="tech_c">
      </div>
      <div>
        <label class="label" for="notify">Notify</label>
        <input type="email" name="notify" id="notify"
               :class="{ email , error: !email.valid }"
               v-model="email.value">
      </div>
      <div>
        <label class="label" for="mnt_irt">Mnt-irt</label>
        <input type="text" name="mnt_irt" id="mnt_irt" v-model="mnt_irt">
      </div>
      <div>
        <label class="label" for="mnt_lower">Mnt-lower</label>
        <input type="text" name="mnt_lower" id="mnt_lower" v-model="mnt_lower">
      </div>
      <div>
        <label class="label" for="mnt_routes">Mnt-routes</label>
        <input type="text" name="mnt_routes" id="mnt_routes" v-model="mnt_routes">
      </div>
      <div>
        <label class="label" for="mnt_by">Mnt-by</label>
        <input type="text" name="mnt_by" id="mnt_by" required="" v-model="mnt_by">
      </div>
      <div>
        <label class="label" for="notify">Changed</label>
        <input type="email" name="notify" id="notify"
               :class="{ changed , error: !changed.valid }"
               v-model="changed.value">
      </div>
      <div>
        <label class="label" for="source">Source</label>
        <input type="text" name="source" id="source" required="" v-model="source">
      </div>
      <div>
        <input type="submit" value="Send Form">
      </div>
    </fieldset>
  </form>
  </div>
</template>

<script>
var emailRegExp = /^[a-zA-Z0-9.!#$%&'*+=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*$/;
export default {
  name: 'AutNumForm',
  props: {
    
  },
  data() {
    return {
      aut_num: "",
      as_name: "",
      member_of: "",
      import_policy: "",
      mp_import: "",
      export_policy: "",
      mp_export: "",
      default_policy: "",
      mp_default: "",
      remarks: "",
      org: "ORG-",
      admin_c: "",
      tech_c: "",
      mnt_irt: "",
      mnt_lower: "",
      mnt_routes: "",
      mnt_by: "",
      source: "",
      changed:{
        value: "test@yopmail.com",
        valid: true
      },
      email: {
        value: "test@yopmail.com",
        valid: true
      },
      selection: {
        status: "0",
        framework: "vue",
        features: []
      },
      description: {
        text: ``,
        // maxlength: 255
      },
      submitted: false
    };
  },
  created(){

  },
  methods: {
    // submit form handler
    submit: function() {
      this.submitted = true;
    },
    // validate by type and value
    validate: function(type, value) {
      if (type === "email") {
        this.email.valid = this.isEmail(value) ? true : false;
      }
    },
    // check for valid email adress
    isEmail: function(value) {
      return emailRegExp.test(value);
    },
    // check or uncheck all
    checkAll: function(event) {
      this.selection.features = event.target.checked ? this.features : [];
    }
  },
  watch: {
    // watching nested property
    "email.value": function(value) {
      this.validate("email", value);
    },
    "changed.value": function(value){
      this.validate("email",value);
    }
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css?family=Source+Code+Pro:300,400");

*,
*::after,
*::before {
  box-sizing: border-box;
}

.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

a {
  color: #2c3e50;
  text-decoration: none;
}

header {
  position: relative;
  height: 150px;
  padding-top: 100px;
}

header h1 {
  text-align: center;
  font-size: 2.4rem;
  font-weight: 300;
}

#app {
  display: flex;
}

.vue-form {
  font-size: 16px;
  width: 500px;
  padding: 15px 30px;
  border-radius: 4px;
  margin: 50px auto;
  width: 500px;
  background-color: #fff;
  box-shadow: 0 4px 6px 0 rgba(0, 0, 0, 0.3);
}
.vue-form fieldset {
  margin: 24px 0 0 0;
}
.vue-form legend {
  padding-bottom: 10px;
  border-bottom: 1px solid #ecf0f1;
}
.vue-form div {
  position: relative;
  margin: 20px 0;
}
.vue-form h4,
.vue-form .label {
  color: #94aab0;
  margin-bottom: 10px;
}
.vue-form .label {
  display: block;
}
.vue-form input,
.vue-form textarea,
.vue-form select,
.vue-form label {
  color: #2b3e51;
}
.vue-form input[type="text"],
.vue-form input[type="email"],
.vue-form textarea,
.vue-form select,
.vue-form legend {
  display: block;
  width: 100%;
  appearance: none;
}
.vue-form input[type="text"],
.vue-form input[type="email"],
.vue-form textarea,
.vue-form select {
  padding: 12px;
  border: 1px solid #cfd9db;
  background-color: #ffffff;
  border-radius: 0.25em;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.08);
}
.vue-form input[type="text"]:focus,
.vue-form input[type="email"]:focus,
.vue-form textarea:focus,
.vue-form select:focus {
  outline: none;
  border-color: #2c3e50;
  box-shadow: 0 0 5px rgba(44, 151, 222, 0.2);
}
.vue-form .select {
  position: relative;
}
.vue-form .select::after {
  content: "";
  position: absolute;
  z-index: 1;
  right: 16px;
  top: 50%;
  margin-top: -8px;
  display: block;
  width: 16px;
  height: 16px;
  background: url("data:image/svg+xml;charset=utf-8,%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22utf-8%22%3F%3E%0D%0A%3C%21DOCTYPE%20svg%20PUBLIC%20%22-%2F%2FW3C%2F%2FDTD%20SVG%201.1%2F%2FEN%22%20%22http%3A%2F%2Fwww.w3.org%2FGraphics%2FSVG%2F1.1%2FDTD%2Fsvg11.dtd%22%3E%0D%0A%3Csvg%20version%3D%221.1%22%20id%3D%22Layer_1%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22%20x%3D%220px%22%20y%3D%220px%22%0D%0A%09%20width%3D%2216px%22%20height%3D%2216px%22%20viewBox%3D%220%200%2016%2016%22%20enable-background%3D%22new%200%200%2016%2016%22%20xml%3Aspace%3D%22preserve%22%3E%0D%0A%3Cg%3E%0D%0A%09%3Cpolygon%20fill%3D%22%232c3e50%22%20points%3D%220.9%2C5.5%203.1%2C3.4%208%2C8.3%2012.9%2C3.4%2015.1%2C5.5%208%2C12.6%20%09%22%2F%3E%0D%0A%3C%2Fg%3E%0D%0A%3C%2Fsvg%3E")
    no-repeat center center;
  pointer-events: none;
}
.vue-form select {
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
  cursor: pointer;
}
.vue-form select::-ms-expand {
  display: none;
}
.vue-form .vue-form-list {
  margin-top: 16px;
}
.vue-form .vue-form-list::after {
  clear: both;
  content: "";
  display: table;
}
.vue-form .vue-form-list li {
  display: inline-block;
  position: relative;
  user-select: none;
  margin: 0 26px 16px 0;
  float: left;
}
.vue-form input[type="radio"],
.vue-form input[type="checkbox"] {
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  margin: 0;
  padding: 0;
  opacity: 0;
  z-index: 2;
}
.vue-form input[type="radio"] + label,
.vue-form input[type="checkbox"] + label {
  padding-left: 24px;
}
.vue-form input[type="radio"] + label::before,
.vue-form input[type="radio"] + label::after,
.vue-form input[type="checkbox"] + label::before,
.vue-form input[type="checkbox"] + label::after {
  content: "";
  display: block;
  position: absolute;
  left: 0;
  top: 50%;
  margin-top: -8px;
  width: 16px;
  height: 16px;
}
.vue-form input[type="radio"] + label::before,
.vue-form input[type="checkbox"] + label::before {
  border: 1px solid #cfd9db;
  background: #ffffff;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.08);
}
.vue-form input[type="radio"] + label::before,
.vue-form input[type="radio"] + label::after {
  border-radius: 50%;
}
.vue-form input[type="checkbox"] + label::before,
.vue-form input[type="checkbox"] + label::after {
  border-radius: 0.25em;
}
.vue-form input[type="radio"] + label::after,
.vue-form input[type="checkbox"] + label::after {
  background-color: #2c3e50;
  background-position: center center;
  background-repeat: no-repeat;
  box-shadow: 0 0 5px rgba(44, 151, 222, 0.4);
  display: none;
}
.vue-form input[type="radio"] + label::after {
  background-image: url("data:image/svg+xml;charset=utf-8,%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22utf-8%22%3F%3E%0D%0A%3C%21DOCTYPE%20svg%20PUBLIC%20%22-%2F%2FW3C%2F%2FDTD%20SVG%201.1%2F%2FEN%22%20%22http%3A%2F%2Fwww.w3.org%2FGraphics%2FSVG%2F1.1%2FDTD%2Fsvg11.dtd%22%3E%0D%0A%3Csvg%20version%3D%221.1%22%20id%3D%22Layer_1%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22%20x%3D%220px%22%20y%3D%220px%22%0D%0A%09%20width%3D%2216px%22%20height%3D%2216px%22%20viewBox%3D%220%200%2016%2016%22%20enable-background%3D%22new%200%200%2016%2016%22%20xml%3Aspace%3D%22preserve%22%3E%0D%0A%3Ccircle%20fill%3D%22%23FFFFFF%22%20cx%3D%228%22%20cy%3D%228%22%20r%3D%223%22%2F%3E%0D%0A%3C%2Fsvg%3E");
}
.vue-form input[type="checkbox"] + label::after {
  background-image: url("data:image/svg+xml;charset=utf-8,%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22utf-8%22%3F%3E%0D%0A%3C%21--%20Generator%3A%20Adobe%20Illustrator%2018.1.1%2C%20SVG%20Export%20Plug-In%20.%20SVG%20Version%3A%206.00%20Build%200%29%20%20--%3E%0D%0A%3C%21DOCTYPE%20svg%20PUBLIC%20%22-%2F%2FW3C%2F%2FDTD%20SVG%201.1%2F%2FEN%22%20%22http%3A%2F%2Fwww.w3.org%2FGraphics%2FSVG%2F1.1%2FDTD%2Fsvg11.dtd%22%3E%0D%0A%3Csvg%20version%3D%221.1%22%20id%3D%22Layer_1%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22%20x%3D%220px%22%20y%3D%220px%22%0D%0A%09%20width%3D%2216px%22%20height%3D%2216px%22%20viewBox%3D%220%200%2016%2016%22%20enable-background%3D%22new%200%200%2016%2016%22%20xml%3Aspace%3D%22preserve%22%3E%0D%0A%3Cpolyline%20fill%3D%22none%22%20stroke%3D%22%23FFFFFF%22%20stroke-width%3D%222%22%20stroke-linecap%3D%22square%22%20stroke-miterlimit%3D%2210%22%20points%3D%225%2C8%207%2C10%2011%2C6%20%22%2F%3E%0D%0A%3C%2Fsvg%3E");
}
.vue-form input[type="radio"]:focus + label::before,
.vue-form input[type="checkbox"]:focus + label::before {
  box-shadow: 0 0 5px rgba(44, 151, 222, 0.6);
}
.vue-form input[type="radio"]:checked + label::after,
.vue-form input[type="checkbox"]:checked + label::after {
  display: block;
}
.vue-form input[type="radio"]:checked + label::before,
.vue-form input[type="radio"]:checked + label::after,
.vue-form input[type="checkbox"]:checked + label::before,
.vue-form input[type="checkbox"]:checked + label::after {
  animation: cd-bounce 0.3s;
}
.vue-form textarea {
  min-height: 120px;
  resize: vertical;
  overflow: auto;
}
.vue-form input[type="submit"] {
  border: none;
  background: #2c3e50;
  border-radius: 0.25em;
  padding: 12px 20px;
  color: #ffffff;
  font-weight: bold;
  float: right;
  cursor: pointer;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  appearance: none;
}
.no-touch .vue-form input[type="submit"]:hover {
  background: #42a2e1;
}
.vue-form input[type="submit"]:focus {
  outline: none;
  background: #2b3e51;
}
.vue-form input[type="submit"]:active {
  transform: scale(0.9);
}
.vue-form .error-message {
  height: 35px;
  margin: 0px;
}
.vue-form .error-message p {
  background: #e94b35;
  color: #ffffff;
  font-size: 1.4rem;
  text-align: center;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  border-radius: 0.25em;
  padding: 16px;
}
.vue-form .error {
  border-color: #e94b35 !important;
}
.vue-form .counter {
  background-color: #ecf0f1;
  position: absolute;
  right: 0px;
  top: 0px;
  font-size: 10px;
  padding: 4px;
}

.debug {
  border-radius: 4px;
  margin: 50px auto;
  width: 500px;
  background-color: #000;
  padding: 50px;
  background: rgba(0, 0, 0, 0.8);
  box-shadow: 0 4px 6px 0 rgba(0, 0, 0, 0.3);
}

.debug pre {
  color: #ffffff;
  font-size: 18px;
  line-height: 30px;
  font-family: "Source Code Pro", monospace;
  font-weight: 300;
  white-space: pre-wrap;
}

@-webkit-keyframes cd-bounce {
  0%,
  100% {
    -webkit-transform: scale(1);
  }
  50% {
    -webkit-transform: scale(0.8);
  }
}
@-moz-keyframes cd-bounce {
  0%,
  100% {
    -moz-transform: scale(1);
  }
  50% {
    -moz-transform: scale(0.8);
  }
}
@keyframes cd-bounce {
  0%,
  100% {
    transform: scale(1);
  }
  50% {
    transform: scale(0.8);
  }
}
</style>
