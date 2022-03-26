<template>
  <div id="auth" class="h-full grid pl-10 pr-10 grid-cols-2 grid-rows-1">
    <div id="accounts-wrapper" class="col-start-1 row-start-1">
      <div class="account-container" v-for="(farm, index) in farms" :key="index">
        <div class="account p-4 bg-gray-200 mt-1 mb-1 hover:bg-gray-300 select-none flex" v-if="!farm.isFarm">
          <div>{{farm.name}}</div>
          <div class="ml-auto">
            <button class="btn">Edit</button>
            <button class="btn">Login</button>
          </div>
        </div>
      </div>
      <div class="controls">
        <button class="btn" @click="createProfileForm">Create</button>
        <button class="btn" @click="refresh">Refresh</button>
      </div>
    </div>
    <div id="edits-wrapper" class="hidden col-start-2 col-end-3 row-start-1">
    </div>
    <div id="right-col-wrapper" class="col-start-2 col-end-3 row-start-1"><svg-icon icon="magelogo" noinvert="true" /></div>
    <div id="profiles-wrapper" class="hidden col-start-1 col-end-3 row-start-1 bg-white">
      <cp />
      <button class="btn" @click="cancelProfileForm">Cancel</button>
    </div>
  </div>
</template>

<script>
import $ from "jquery";
import cp from "@/components/CreateProfile";
import SvgIcon from "@/components/SvgIcon";

export default {
    data() {
        return {
            farms: [],
            helpPage: "dev"
        };
    },

    methods: {
        createProfileForm() {
            $("#profiles-wrapper").removeClass("hidden");
        },

        cancelProfileForm() {
            $("#profiles-wrapper").addClass("hidden");
        },

        refresh() {
          location.reload();
        }
    },

    created: async function() {
        this.farms = await window.api.remote("getAuthSystemList");
    },

    components: { cp, SvgIcon },
};
</script>

<style>
  .btn {
    @apply bg-gray-400 text-gray-100 p-1 rounded-md ml-1 hover:bg-gray-600;
  }
</style>
