<template>
  <section id="posts">
    <PostPreview 
    v-for="post in posts" 
    :key="post.id"
    :title="post.title"
    :excerpt="post.previewText"
    :thumbnailUrl="post.thumbnailUrl"
    :id="post.id"
    />
  </section>
</template>

<script>
import PostPreview from "@/components/PostPreview";
export default {
  components: {
    PostPreview
  },
  asyncData(context) {
    return context.app.$storyapi.get('cdn/stories', {
      version: 'draft',
      starts_with: 'blog/'
    }).then(res => {
   
      return { 
        posts: res.data.stories.map(bp => {
          return {
            id: bp.slug,
            title: bp.content.title,
            previewText: bp.content.summery,
            thumbnailUrl: bp.content.thumbnail
          }
        })
      };
    });
  }
  // data() {
  //   return {
  //     posts: [
  //       {
  //         title: 'A New Beginning',
  //         previewText: 'This will be awesome, don\'t miss it',
  //         thumbnailUrl: 'https://media2.s-nbcnews.com/j/newscms/2018_15/1331890/horiatiki-greek-salad-today-041618-tease_79c5041ae6a58da5e333029bbe2c4b88.today-inline-large.jpg',
  //         id: 'a-new-beginning'
  //       },
  //       {
  //         title: 'A Second Beginning',
  //         previewText: 'This will be awesome, don\'t miss it',
  //         thumbnailUrl: 'https://media2.s-nbcnews.com/j/newscms/2018_15/1331890/horiatiki-greek-salad-today-041618-tease_79c5041ae6a58da5e333029bbe2c4b88.today-inline-large.jpg',
  //         id: 'a-second-beginning'
  //       }
  //     ]
  //   };
  // }
};
</script>

<style scoped>
#posts {
  padding-top: 2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

@media (min-width: 55rem) {
  #posts {
    flex-direction: row;
  }
}
</style>
