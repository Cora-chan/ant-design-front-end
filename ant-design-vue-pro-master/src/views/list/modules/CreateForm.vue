<template>
  <a-modal
    title="Create Trading Account"
    :width="640"
    :visible="visible"
    :confirmLoading="loading"
    @ok="() => { $emit('ok') }"
    @cancel="() => { $emit('cancel') }"
  >
    <a-spin :spinning="loading">
      <a-form :form="form" v-bind="formLayout" layout="vertical">
        <!-- 检查是否有 id 并且大于0，大于0是修改。其他是新增，新增不显示主键ID -->
        <a-form-item v-show="model && model.id > 0" label="主键ID">
          <a-input v-decorator="['id', { initialValue: 0 }]" disabled />
        </a-form-item>
        <a-form-item label="Accout Name:">
          <a-input placeholder="Must match forex factory's account name)" />
        </a-form-item>
        <a-form-item label="Accout Number (Eg:MT4 Account Number):">
          <a-input v-decorator="['description']" placeholder="Account Number" />
        </a-form-item>
        <a-form-item label="Starting Balance:">
          <a-input v-decorator="['description']" placeholder="0" />
        </a-form-item>
        <a-form-item label="Trading Account Type:">
          <a-select default-value="0">
            <a-select-option value="0">Demo Account</a-select-option>
            <a-select-option value="1">1</a-select-option>
            <a-select-option value="2">2</a-select-option>
          </a-select>
        </a-form-item>
        <a-form-item label="Broker(Eg:Easy Markets/Vantage FX/IG):">
          <a-select default-value="0">
            <a-select-option value="0">Easy Markets</a-select-option>
            <a-select-option value="1">1</a-select-option>
            <a-select-option value="2">2</a-select-option>
          </a-select>
        </a-form-item>
        <a-form-item label="Default Status for Account:">
          <a-select default-value="0">
            <a-select-option value="0">Active</a-select-option>
            <a-select-option value="1">1</a-select-option>
            <a-select-option value="2">2</a-select-option>
          </a-select>
        </a-form-item>
        <a-form-item label="Strategy Type:">
          <a-select default-value="0">
            <a-select-option value="0">Demo</a-select-option>
            <a-select-option value="1">1</a-select-option>
            <a-select-option value="2">2</a-select-option>
          </a-select>
        </a-form-item>
        <a-form-item label="Default if Individual:">
          <a-select placeholder="No" default-value="0">
            <a-select-option value="0">No</a-select-option>
            <a-select-option value="1">1</a-select-option>
            <a-select-option value="2">2</a-select-option>
          </a-select>
        </a-form-item>
      </a-form>
    </a-spin>
  </a-modal>
</template>

<script>
import pick from 'lodash.pick'

// 表单字段
const fields = ['description', 'id']

export default {
  props: {
    visible: {
      type: Boolean,
      required: true
    },
    loading: {
      type: Boolean,
      default: () => false
    },
    model: {
      type: Object,
      default: () => null
    }
  },
  data () {
    this.formLayout = {
      labelCol: {
        xs: { span: 24 },
        sm: { span: 7 }
      },
      wrapperCol: {
        xs: { span: 24 },
        sm: { span: 13 }
      }
    }
    return {
      form: this.$form.createForm(this)
    }
  },
  created () {
    console.log('custom modal created')

    // 防止表单未注册
    fields.forEach(v => this.form.getFieldDecorator(v))

    // 当 model 发生改变时，为表单设置值
    this.$watch('model', () => {
      this.model && this.form.setFieldsValue(pick(this.model, fields))
    })
  }
}
</script>
