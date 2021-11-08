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

const ydoc = new Y.Doc()

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
      content: `
        <p>
          Hi there,
        </p>
        <p>
          this is a <em>basic</em> example of <strong>Tiptap</strong>. Sure, there are all kind of basic text styles you’d probably expect from a text editor. But wait until you see the lists:
        </p>
        <ul>
          <li>
            That’s a bullet list with one …
          </li>
          <li>
            … or two list items.
          </li>
        </ul>
        <p>
          Isn’t that great? And all of that is editable. But wait, there’s more. Let’s try a code block:
        </p>
        <pre><code class="language-css">body {
  display: none;
}</code></pre>
        <p>
          I know, I know, this is impressive. It’s only the tip of the iceberg though. Give it a try and click a little bit around. Don’t forget to check the other examples too.
        </p>
        <blockquote>
          Wow, that’s amazing. Good work, boy! 👏
          <br />
          — Mom
        </blockquote>
      `,
    })
  },

  beforeUnmount() {
    this.editor.destroy()
    this.anotherEditor.destroy()
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