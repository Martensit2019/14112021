<template>
  <div>
    <div class="top">
      <h1 class="text-uppercase">{{ $t(isCreating() ? "create" : "edit") }}</h1>
    </div>
    000{{product}}
    <ValidationObserver
      ref="product_observer"
      v-slot="{ invalid, handleSubmit }"
    >
      <form @submit.prevent="handleSubmit(save)">
        <input-field
          label="Наименование"
          validation-name="name"
          v-model="product.name"
        />
        <input-field
          label="Артикул"
          validation-name="article"
          v-model="product.article"
        />
        <input-field
          label="Гидравлическое сечение"
          validation-name="hydraulic_section"
          v-model="product.hydraulic_section"
        />
        <input-field
          label="Гидравлическая высота"
          validation-name="hydraulic_height"
          v-model="product.hydraulic_height"
        />
        <input-field
          label="параметр R или α (в зависимости от формы сечения)"
          validation-name="R_param"
          v-model="product.R_param"
        />
        <input-field
          label="Полная высота"
          validation-name="full_height"
          v-model="product.full_height"
        />
        <input-field
          label="Максимальная степень наполнения"
          validation-name="max_fill"
          v-model="product.max_fill"
        />
        <select-field
          label="Материал лотка"
          validation-name="tray_material"
          v-model="product.tray_material"
          :options="materialOptions"
          placeholder="Выберите материал"
        />
        <input-field
          label="Группа лотков"
          validation-name="trays_group"
          v-model="product.trays_group"
        />
        <checkbox-field
          label="Основная высота"
          validation-name="main_height"
          v-model="product.main_height"
        />
        <checkbox-field
          label="Класс A15"
          validation-name="class_A15"
          v-model="product.class_A15"
        />
        <checkbox-field
          label="Класс B125"
          validation-name="class_B125"
          v-model="product.class_B125"
        />
        <checkbox-field
          label="Класс C250"
          validation-name="class_C250"
          v-model="product.class_C250"
        />
        <checkbox-field
          label="Класс D400"
          validation-name="class_D400"
          v-model="product.class_D400"
        />
        <checkbox-field
          label="Класс E600"
          validation-name="class_E600"
          v-model="product.class_E600"
        />
        <checkbox-field
          label="Класс F900"
          validation-name="class_F900"
          v-model="product.class_F900"
        />
        <input-field
          label="Активен"
          validation-name="active"
          v-model="product.active"
        />
        <!-- <checkbox-field
          label="Активен"
          validation-name="active"
          v-model="product.active"
        /> -->
        <checkbox-field
          label="Открытый лоток"
          validation-name="tray_open"
          v-model="product.tray_open"
        />
        <input-field
          label="Форма сечения"
          validation-name="sectional_shape"
          v-model="product.sectional_shape"
        />
        <file-field 
        label="Загрузить новый рисунок"
        v-model="product.img"
        />

        <div class="group-btns">
          <button class="btn" type="submit">
            {{ $t(isCreating() ? "create" : "save") }}
          </button>
          <nuxt-link
            v-if="product.id"
            :to="{ name: 'admin-regions-id', params: { id: product.id } }"
            class="btn"
            >{{ $t("back") }}</nuxt-link
          >
          <nuxt-link v-else :to="{ name: 'admin-regions' }" class="btn">{{
            $t("back")
          }}</nuxt-link>
        </div>
      </form>
    </ValidationObserver>
  </div>
</template>

<script>
import ViewField from "@/components/forms/includes/ViewField";
import InputField from "@/components/forms/includes/InputField";
import SelectField from "@/components/forms/includes/SelectField";
import CheckboxField from "@/components/forms/includes/CheckboxField";
import FileField from "@/components/forms/includes/FileField";

import VueSpinner from "@/components/vueSpinner";
import { ValidationObserver, ValidationProvider } from "vee-validate";
// import {  } from '@/src/queries'
import { mapGetters } from "vuex";
import DateField from "@/components/forms/includes/DateField";
export default {
  name: "TraysPvForm",
  components: {
    DateField,
    CheckboxField,
    SelectField,
    ViewField,
    InputField,
    VueSpinner,
    FileField,
    ValidationObserver,
    ValidationProvider
  },
  props: {
    product: {
      type: Object,
      required: false
    }
  },
  data() {
    return {
      materialOptions: [
        { name: "бетон", id: 0 },
        { name: "полимербетон", id: 1 },
        { name: "пластик", id: 2 }
      ]
    };
  },
  // computed: {
  //   ...mapGetters({
  //     roles: "roles/notClientRoles"
  //   })
  // },
  methods: {
    isCreating() {
      return !this.product.hasOwnProperty("id");
    },
    save() {
      this.$emit("save");
    },
    isFieldDisabled(field) {
      if (!this.fields.hasOwnProperty(field)) return false;
      return !this.fields[field];
    }
  }
};
</script>
