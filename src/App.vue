<template >
  <div id="app" class="fundo">
    <img class="logo" src="img/logo-white3.png" alt="Logo">
    <ul id="menu">
      <li data-menuanchor="page1" class="active">
        <a href="#page1">Section 1</a>
      </li>
      <li data-menuanchor="page2">
        <a href="#page2">Section 2</a>
      </li>
      <li data-menuanchor="page3">
        <a href="#page3">Section 3</a>
      </li>
      <li></li>
    </ul>
    <full-page :options="options" id="fullpage">
      <div class="section">

       <div id="footer">
            <p style="text-align: center">
                CAMPO GRANDE
                <br>
                (67) 3041.8888 | 3326.3079
                <br>
                CONTATO@MASCARENHASBARBOSA.COM.BR
                <br>
                RUA ALAGOAS, 365 - JARDIM DOS ESTADOS
                <br>
                BRASÍLIA | CUIABÁ | GÔIANIA | PALMAS
            </p>
    </div>
    <footer class="footer"></footer>

      </div>
      <div class="section">
        <h3>Section 2</h3>
      </div>
      <div class="section">
        <h3>Section 3</h3>
      </div>
    </full-page>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      options: {
        afterLoad: this.afterLoad,
        scrollOverflow: true,
        scrollBar: false,
        menu: "#menu",
        navigation: true,
        anchors: ["page1", "page2", "page3"]
        //   sectionsColor: ['#41b883', '#ff5f45', '#0798ec', '#fec401', '#1bcee6', '#ee1a59', '#2c3e4f', '#ba5be9', '#b4b8ab']
      }
    };
  },
  methods: {
    afterLoad() {
      console.log("After load");
    },

    addSection(e) {
      e.preventDefault();
      var newSectionNumber =
        document.querySelectorAll(".fp-section").length + 1;

      // creating the section div
      var section = document.createElement("div");
      section.className = "section";
      section.innerHTML = `<h3>Section ${newSectionNumber}</h3>`;

      // adding section
      document.querySelector("#fullpage").appendChild(section);

      // creating the section menu element
      var sectionMenuItem = document.createElement("li");
      sectionMenuItem.setAttribute(
        "data-menuanchor",
        "page" + newSectionNumber
      );
      sectionMenuItem.innerHTML = `<a href="#page${newSectionNumber}">Section${newSectionNumber}</a>`;

      // adding it to the sections menu
      var sectionsMenuItems = document.querySelector("#menu");
      sectionsMenuItems.appendChild(sectionMenuItem);

      // adding anchor for the section
      this.options.anchors.push(`page${newSectionNumber}`);

      // we have to call `update` manually as DOM changes won't fire updates
      // requires the use of the attribute ref="fullpage" on the
      // component element, in this case, <full-page>
      // ideally, use an ID element for that element too
      this.$refs.fullpage.build();
    },
    removeSection() {
      var sections = document
        .querySelector("#fullpage")
        .querySelectorAll(".fp-section");
      var lastSection = sections[sections.length - 1];

      // removing the last section
      lastSection.parentNode.removeChild(lastSection);

      // removing the last anchor
      this.options.anchors.pop();

      // removing the last item on the sections menu
      var sectionsMenuItems = document.querySelectorAll("#menu li");
      var lastItem = sectionsMenuItems[sectionsMenuItems.length - 1];
      lastItem.parentNode.removeChild(lastItem);
    },
    toggleNavigation() {
      this.options.navigation = !this.options.navigation;
    },
    toggleScrollbar() {
      console.log("Changing scrollbar...");
      this.options.scrollBar = !this.options.scrollBar;
    }
  }
};
</script>

<style>
ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
.fundo {
  background-blend-mode: multiply;
  background-image: linear-gradient(
      to right,
      rgb(50, 51, 47),
      rgb(178, 178, 184)
    ),
    url("http://mascarenhasbarbosa.com.br/img/bg_site2.jpg");
}
.logo {
  height: 100px;
  width: auto;
  display: inline-block;
  position: absolute;
}
#footer{
       
    background: url(http://mascarenhasbarbosa.com.br/img/bg_footer.png) repeat-x;
    color: #dedede;
    text-align: center;
        height: 132px;
    
	bottom: 0;
}
.footer,
    .push {
      height: 50px;
    }



</style>
