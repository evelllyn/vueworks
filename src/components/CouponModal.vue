<template>
  <div class="modal fade" id="couponModal" tabindex="-1"
    aria-labelledby="exampleModalLabel" aria-hidden="true" ref="modal">
    <div class="modal-dialog modal-xl" role="document">
      <div class="modal-content border-0">
        <div class="modal-header bg-dark text-white">
          <h5 class="modal-title" id="exampleModalLabel">優惠券</h5>
          <button type="button" class="btn-close"
                  data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <div class="mb-3">
            <label for="title">優惠券</label>
            <input type="text" class="form-control" id="title" v-model="tempCoupon.title"
                    placeholder="請輸入優惠券名稱">
          </div>
          <div class="mb-3">
            <label for="coupon_code">優惠碼</label>
            <input type="text" class="form-control" id="coupon_code" v-model="tempCoupon.code"
                    placeholder="請輸入優惠碼">
          </div>
          <div class="mb-3">
            <label for="due_date">到期日</label>
            <input type="date" class="form-control" id="due_date" v-model="due_date">
          </div>
          <div class="mb-3">
            <label for="price">折扣</label>
            <input type="number" class="form-control" id="price" v-model.number="tempCoupon.percent"
                    placeholder="請輸入折扣百分比">
          </div>
          <div class="mb-3">
            <div class="form-check">
              <input class="form-check-input" type="checkbox"
                      :true-value="1"
                      :false-value="0"
                      id="is_enabled" v-model="tempCoupon.is_enabled">
              <label class="form-check-label" for="is_enabled">
                是否啟用
              </label>
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-outline-secondary"
                  data-bs-dismiss="modal">關閉
          </button>
          <button type="button" class="btn btn-primary" @click="$emit('update-coupon',  tempCoupon)">更新優惠券</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import modalMixin from '@/mixins/modalMixin'

export default {
  props: {
    coupon: {}
  },
  watch: {
    coupon () {
      this.tempCoupon = this.coupon
      const dateAndTime = new Date(this.tempCoupon.due_date * 1000)
        .toISOString().split('T')
      this.due_date = dateAndTime[0]
    },
    due_date () {
      this.tempCoupon.due_date = Math.floor(new Date(this.due_date) / 1000)
    }
  },
  data () {
    return {
      tempCoupon: {},
      due_date: ''
    }
  },
  emits: ['update-coupon'],
  mixins: [modalMixin]
}
</script>
