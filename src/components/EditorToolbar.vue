<template>
  <div v-if="editor">
        <button @click="editor.chain().focus().toggleHeading({ level: 1 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 1 }) }">
            H1
        </button>
        <button @click="editor.chain().focus().toggleHeading({ level: 2 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 2 }) }">
            H2
        </button>

        <button @click="editor.chain().focus().toggleBold().run()" :class="{ 'is-active': editor.isActive('bold') }">
            Bold
        </button>
        <button @click="editor.chain().focus().toggleItalic().run()" :class="{ 'is-active': editor.isActive('italic') }">
            Italic
        </button>

        <button @click="editor.chain().focus().setParagraph().run()" :class="{ 'is-active': editor.isActive('paragraph') }">
            Paragraph
        </button>

        <button @click="editor.chain().focus().undo().run()">
            Undo
        </button>
        <button @click="editor.chain().focus().redo().run()">
            Redo
        </button>
      </div>
    </template>

    <script>
    export default {
      props: {
        editor: {
          default: null,
        }
      }
    }
    </script>