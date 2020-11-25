<template>
    <div class="flex h-full">
        <ChatUserList 
            :current-user="currentUser"
            :chat-with="chatWith"
            @updatedChatWith="updatedChatWith"
        />

        <div v-if="chatWith" class="w-4/5 flex flex-col">
            <ChatArea 
                :chat-id="chatWith"
                :messages="messages"
            />
            <div class="flex-initial p-2">
                <input 
                    class="border-2border-solid rounnded border-gray-600 w-full p-3"
                    type="text"
                    @keyup.enter="submit"
                    v-model="text"
                />
            </div>
        </div>
        <div v-else class="p-3">
            Please choose the chat member
        </div>
    </div>
</template>

<script>
    import ChatUserList from './ChatUserList';
    import ChatArea from './ChatArea';

    export default {
        props: {
            currentUser: {
                type: Number,
                required: true
            }
        },
        components: {
            ChatUserList,
            ChatArea
        },

        data() {
            return {
                chatWith: null,
                text: '',
                messages: []
            }
        },

        created() {
            window.Echo.private('chats').listen('MessageSent', e=> {
                if(e.message.to === this.currentUser && e.message.from === this.chatWith) {
                    this.messages.push(e.message);
                }
            })
        },

        mounted() {
            console.log('Component mounted.')
        },

        methods: {
            updatedChatWith(value) {
                this.chatWith = value;
                this.getMessages()
            },

            getMessages() {
                axios.get('/api/messages', {
                    params: {
                        to: this.chatWith,
                        from: this.currentUser
                    }
                }).then(res=>{
                    this.messages = res.data.messages
                }).catch(err=>{
                    console.log(error)
                })
            },

            submit() {
                if(this.text){
                    axios.post('/api/messages', {
                        text: this.text,
                        to: this.chatWith,
                        from: this.currentUser
                    }).then(res=>{
                        this.messages.push(res.data.message)
                    })
                }
                this.text = '';
            }
        }
    }
</script>
