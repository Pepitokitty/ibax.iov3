<template>
  <div class="user-rules">
    <div class="user-rules-img">
      <img src="@/assets/images/login/rules.png" alt="rules" />
    </div>
    <h6 class="title-h6">How to Get IBXC</h6>
    <h6 class="title-h6">A. Join Developer Community and Earn IBXC</h6>
    <div class="user-rules-content">
      <div class="user-rules-content-item">
        <div class="user-rules-content-item-big">1</div>
        <div class="user-rules-content-item-text">
          <p>SUBMIT</p>
          <p>A Development Request (Bug/New Idea /Existing issue)</p>
        </div>
      </div>
      <div class="user-rules-content-item">
        <div class="user-rules-content-item-big">2</div>
        <div class="user-rules-content-item-text">
          <p>GET</p>
          <p>Approved</p>
        </div>
      </div>
      <div class="user-rules-content-item">
        <div class="user-rules-content-item-big">3</div>
        <div class="user-rules-content-item-text">
          <p>COMPLETE</p>
          <p>The Development and Submit the solution</p>
        </div>
      </div>
      <div class="user-rules-content-item">
        <div class="user-rules-content-item-big">4</div>
        <div class="user-rules-content-item-text">
          <p>CLAIM</p>
          <p>Your Reward</p>
        </div>
      </div>
    </div>
    <h6 class="title-h6">B. Join IBAX User Community and Earn IBXC</h6>
    <div class="user-rules-content">
      <div class="user-rules-content-item">
        <div class="user-rules-content-item-big">1</div>
        <div class="user-rules-content-item-text">
          <p>JOIN</p>
          <p>IBAX Community</p>
        </div>
      </div>
      <div class="user-rules-content-item">
        <div class="user-rules-content-item-big">2</div>
        <div class="user-rules-content-item-text">
          <p>FINISH</p>
          <p>Task</p>
        </div>
      </div>
      <div class="user-rules-content-item">
        <div class="user-rules-content-item-big">3</div>
        <div class="user-rules-content-item-text">
          <p>GET</p>
          <p>IBAX points</p>
        </div>
      </div>
      <div class="user-rules-content-item">
        <div class="user-rules-content-item-big">4</div>
        <div class="user-rules-content-item-text">
          <p>REDEEM</p>
          <p>To IBXC</p>
        </div>
      </div>
    </div>
    <h6 class="title-h6">IBAX Ranking System</h6>
    <div class="user-rules-table-box">
      <table ref="tableRules" class="user-rules-table">
        <thead>
          <tr>
            <th>Title</th>
            <th>Exp</th>
            <th>Monthly Reward Pool</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in arrHonor" :key="item.id">
            <td>
              <img
                class="user-rules-table-header"
                :src="`${baseUrl}${item.title_icon}`"
                :onerror="defaultImg"
                alt="title_icon"
              />
              <span>{{ item.title }}</span>
            </td>
            <td>
              <span>{{ money_format(item.points_start) }}</span>
              <span class="user-rules-table-box-item-line-odd">/</span>
              <span>{{ money_format(item.points_end) }}</span>
            </td>
            <td>
              <span class="user-rules-table-box-item-line-odd">{{
                money_format(item.monthly_reward_pool)
              }}</span>
              <img
                class="user-rules-table-reward"
                :src="`${baseUrl}${item.reward_icon}`"
                :onerror="defaultImg"
                alt="reward_icon"
              />
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
export default {
  props: {},
  data() {
    return {
      arrHonor: [],
      objHonor: {
        type: 2,
        language_type: 1
      }
    };
  },
  computed: {
    defaultImg() {
      return (
        'this.src="' + require('../assets/images/login/task-error.png') + '"'
      );
    }
  },
  watch: {},
  created() {},
  mounted() {
    this.handleGithubTitleList(this.objHonor);
  },
  methods: {
    async handleGithubTitleList(params) {
      const res = await this.$axios.$post('/github_title_list', params);
      console.log(JSON.stringify(res));
      if (res.code === 0 && res.data) {
        this.arrHonor = res.data;
      } else {
        this.arrHonor = [];
      }
    }
  }
};
</script>
