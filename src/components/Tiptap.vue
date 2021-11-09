<template>
  <h1>Editor</h1>
  <div class="editor">
    <editor-toolbar :editor="editor" />
    <editor-content :editor="editor" />
  </div>
  <h1>Another Editor</h1>
  <div class="editor">
    <editor-toolbar :editor="anotherEditor" />
    <editor-content :editor="anotherEditor" />
  </div>
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'
import EditorToolbar from './EditorToolbar.vue'
import Collaboration from '@tiptap/extension-collaboration'
import * as Y from 'yjs'
import { HocuspocusProvider } from '@hocuspocus/provider'

const ydoc = new Y.Doc()
const provider = new HocuspocusProvider({
  document: ydoc,
  url: 'wss://connect.tiptap.dev',
  name: 'foobar.123',
  broadcast: false,
})

export default {
  components: {
    EditorContent,
    EditorToolbar,
  },

  data() {
    return {
      editor: null,
      anotherEditor: null,
    }
  },

  mounted() {
    this.anotherEditor = new Editor({
      extensions: [
        StarterKit.configure({
          history: false,
        }),
        Collaboration.configure({
          document: ydoc,
        }),
      ],
    })

    this.editor = new Editor({
      extensions: [
        StarterKit.configure({
          history: false,
        }),
        Collaboration.configure({
          document: ydoc,
        }),
      ],
    })
  },

  beforeUnmount() {
    this.editor.destroy()
    this.anotherEditor.destroy()
    provider.destroy()
  },
}
</script>

<style lang="scss">
body {
  font-family: sans-serif;
  font-size: 18px;
  margin: 2rem;
}

button {
  border: 1px solid black;
  border-radius: 0.25rem;
  background-color: white;
  margin-right: 0.2rem;
  font-size: 1rem;
  padding: 0.2rem 0.4rem;

  &.is-active {
    background-color: black;
    color: white;
  }
}

.editor {
  border: 3px solid #dee2e6;
  border-radius: 0.75rem;
  padding: 1rem;
  margin: 1rem 0;
}

/* Basic editor styles */
.ProseMirror {
  > * + * {
    margin-top: 0.75em;
  }

  ul,
  ol {
    padding: 0 1rem;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    line-height: 1.1;
  }

  code {
    background-color: rgba(#616161, 0.1);
    color: #616161;
  }

  pre {
    background: #0D0D0D;
    color: #FFF;
    font-family: 'JetBrainsMono', monospace;
    padding: 0.75rem 1rem;
    border-radius: 0.5rem;

    code {
      color: inherit;
      padding: 0;
      background: none;
      font-size: 0.8rem;
    }
  }

  img {
    max-width: 100%;
    height: auto;
  }

  blockquote {
    padding-left: 1rem;
    border-left: 2px solid rgba(#0D0D0D, 0.1);
  }

  hr {
    border: none;
    border-top: 2px solid rgba(#0D0D0D, 0.1);
    margin: 2rem 0;
  }
}
</style>