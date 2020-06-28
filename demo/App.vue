<script>
import { FocusTrap } from "/@src/";

export default {
  components: { FocusTrap },
  data() {
    return {
      demos: {
        basic: {
          isActive: false
        },
        iene: {
          initialFocus: function initialFocus () {
            return this.$refs.ieneInput
          }.bind(this),
          isActive: false
        }
      }
    }
  },
}
</script>

<template>
  <h1 tabindex="0">focus-trap demo</h1>

  <p>
    <span style="font-size:2em;vertical-align:middle;">☜</span>
    <a
      href="https://github.com/posva/focus-trap-vue"
      style="vertical-align:middle;"
    >Return to the repository</a>
  </p>

  <p>
    In the demos below, you'll be able to tell that a focus trap is active
    because it will turn pink. You should also be able to tell because it
    will trap your focus!
  </p>

  <p>
    When a trap is active, you can deactivate it by pushing its deactivate
    button or, if the demo allows, hitting
    <kbd>Escape</kbd>.
  </p>

  <section id="basic">
    <h2>default behavior</h2>
    <p>
      <button
        id="activate-default"
        @click="demos.basic.isActive = true"
      >activate trap</button>
    </p>

    <focus-trap v-model="demos.basic.isActive">
      <div
        id="default"
        class="trap"
        :class="demos.basic.isActive && 'is-active'"
        tabindex="-1"
      >
        <p>
          Here is a focus trap
          <a href="#">with</a>
          <a href="#">some</a>
          <a href="#">focusable</a> parts.
        </p>
        <p>
          <button
            id="deactivate-default"
            @click="demos.basic.isActive = false"
          >deactivate trap</button>
        </p>
      </div>
    </focus-trap>
  </section>

  <section id="iene">
    <h2 id="iene-heading">initial element, no escape</h2>
    <p>
      When this focus trap activates, focus jumps to a specific, manually
      specified element.
    </p>
    <p>
      Also, in this demo the
      <kbd>Escape</kbd> key does not deactivate the
      focus trap. You must click the button.
    </p>
    <p>
      <button @click="demos.iene.isActive = true">activate trap</button>
    </p>

    <focus-trap
      v-model="demos.iene.isActive"
      :initial-focus="demos.iene.initialFocus"
    >
      <div
        class="trap"
        :class="demos.iene.isActive && 'is-active'"
      >
        <p>
          Here is a focus trap
          <a href="#">with</a>
          <a href="#">some</a>
          <a href="#">focusable</a> parts.
        </p>
        <p>
          <label class="inline-label">
            Initially focused input
            <input ref="ieneInput" />
          </label>
        </p>
        <p>
          <button @click="demos.iene.isActive = false">deactivate trap</button>
        </p>
      </div>
    </focus-trap>
  </section>
</template>

<style>
body {
  color: #333;
  font-family: "Helvetica Neue", "Helvetica", Helvetica, Arial, sans-serif;
  font-size: 14px;
  line-height: 1.4;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  max-width: 600px;
  margin: 0 auto 200px;
  padding: 10px;
}

*:focus {
  outline: 5px solid lightblue;
}

.trap {
  border: 1px solid #ccc;
  padding: 1em 2em;
}

.trap.is-active {
  background: #fee9ff;
}

.inline-label {
  margin-right: 0.5em;
}

#demo-four,
#initial-nine {
  outline: 0;
}

code,
kbd {
  background: #eee;
  font-size: 90%;
  padding: 0 2px;
}
</style>