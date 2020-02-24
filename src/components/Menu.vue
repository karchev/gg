<template>
  <div>
    <ul id="navigation">
      <li v-for="item in navList" v-bind:key="item">
        <template v-if="item.children">
          <a
            :href="item.url"
            :title="item.name"
            @click="item.isOpen = !item.isOpen, item.active = !item.active"
            :class="{ active : item.active }"
          >{{ item.name }}</a>
          <div :class="{ isOpen : item.isOpen }" class="dropdown">
            <ul>
              <li v-for="{ url, name, index, target } in item.children" :key="index">
                <a :href="url" :title="name" :target="target">{{ name }}</a>
              </li>
            </ul>
          </div>
        </template>
        <template v-else>
          <a :href="item.url" :title="item.name">{{ item.name }}</a>
        </template>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Menu",
  data() {
    return {
      navList: [
        { url: "#", name: "골든글러브" },
        {
          url: "#",
          name: "오늘의 시합",
          children: [
            {
              url: "#",
              name: "오늘의 시합",
              target: "_blank"
            },
            {
              url: "#",
              name: "시합 검색",
              target: "_blank"
            },
            {
              url: "#",
              name: "나의 시합",
              target: "_blank"
            }
          ],
          isOpen: false,
          active: false
        },
        { url: "#", name: "선수" },
        { url: "#", name: "팀" },
        { url: "#", name: "리그" },
        {
          url: "#",
          name: "야구광장",
          children: [
            {
              url: "#",
              name: "야구광장",
              target: "_blank"
            },
            {
              url: "#",
              name: "공지사항",
              target: "_blank"
            }
          ],
          isOpen: false,
          active: false
        }
      ]
    };
  }
};
</script>

<style lang="scss" scoped>

$black: #212529;
$white: #ffffff;

$col1: #9f1414;
$col2: #dc3545;

*,
::before,
::after {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

@mixin flex($fd: row, $jc: center, $ai: center) {
  display: flex;
  flex-direction: $fd;
  justify-content: $jc;
  align-items: $ai;
}

ul {
  list-style-type: none;

  li {
    position: relative;
    margin: 1.5%;
    
    text-align: center;

    a {
      display: block;
      padding: 0.55em 1em;
      text-decoration: none;
      color: $black;
      transition: all 200ms ease;

      &:hover {
        color: $white;
        background-color: rgba($black, 0.65);
      }

      &.active {
        background-color: rgba($black, 0.45);
      }
    }

    ul {
      li {
        a {
          background-color: transparent;
        }
      }
    }
  }

  &#navigation {
    @include flex($ai: flex-start);
  }
}

.dropdown { 
  position: relative;
  left: 50%;
  transform: translatex(-50%) rotatex(90deg) scale(0);
  margin-top: 0.55em;
  transform-origin: 0 0;
  border-radius: 0.35em;
  visibility: hidden;
  opacity: 0;
  transition: all 200ms linear;

  &.isOpen {
    transform: translatex(-50%);
    visibility: visible;
    opacity: 1;
  }
}

</style>
