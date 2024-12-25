<template>
     <div>
       <h1>Мои заметки</h1>
       <input v-model="newNote.title" placeholder="Название заметки" />
       <textarea v-model="newNote.content" placeholder="Содержимое заметки"></textarea>
       <input type="checkbox" v-model="newNote.important" />
       <label>Пометить как важное</label>
       <button @click="addNote" :style="add">Добавить заметку</button>
       <button @click="saveNote" :style="change">Сохранить</button>
       <button @click="cancelChange" :style="change">Отменить</button>

       <ul>
         <li v-for="(note, index) in notes" :key="index" :style="notestyle">
           <h3 v-if="note.important==true" :style="{ color: 'red'}">{{ note.title }}</h3>
           <h3 v-else>{{ note.title }}</h3>
           <p>{{ note.content }}</p>
           <div>
            <button @click="deleteNote(index)">Удалить</button>
            <button @click="changeNote(index)">Изменить</button>
           </div>
         </li>
       </ul>
     </div>
   </template>

   <script>
   export default {
     data() {
       return {
         newNote: {
           title: '',
           content: '',
           important:''
         },
         notes: [],
         changeindex:0,
         change: {display:'none'},
         add:{display:'inline'},
         notestyle:{
          border:'black solid 1px',
          width:'wrap_content',
          height:'wrap_content',
          padding:'20px'
         }
       };
     },
     methods: {
       addNote() {
         if (this.newNote.title && this.newNote.content) {
           this.notes.push({ ...this.newNote });
           this.newNote.title = '';
           this.newNote.content = '';
           this.newNote.important='';
         } else {
           alert('Пожалуйста, заполните название и содержимое заметки.');
         }
       },
       deleteNote(index) {
         this.notes.splice(index, 1);
       },
       changeNote(index){
         this.newNote.title=this.notes[index].title;
         this.newNote.content=this.notes[index].content;
         this.newNote.important=this.notes[index].important;
         this.change.display='inline';
         this.add.display='none';
         this.changeindex=index;
       },
       cancelChange(){
         this.newNote.title="";
         this.newNote.content="";
         this.newNote.important="";
         this.change.display='none';
         this.add.display='inline';
       },
       saveNote(){
         this.notes[this.changeindex].title=this.newNote.title;
         this.notes[this.changeindex].content=this.newNote.content;
         this.notes[this.changeindex].important=this.newNote.important;
         this.cancelChange();
       }
     }
   };
   </script>