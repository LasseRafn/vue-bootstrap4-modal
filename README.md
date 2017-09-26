# vue-bootstrap4-modal
Vue Bootstrap 4 Modal Component

## Usage

``` vue
<modal title="Hello World" cancel-button-text="Cancel" submit-button-text="Hello" :is-small="true" v-if="show_modal" @close="show_modal = false" @submit="alert('Done!');" >
  Hello.
</modal>
```
