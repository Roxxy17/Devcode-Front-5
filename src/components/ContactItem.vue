<template>
  <div data-cy="item-card" class="contact-item__wrapper">
    <div class="contact-item__first-row">
      <p data-cy="item-name" class="contact-item__name">{{ full_name }}</p>
      <div class="contact-item__button-wrapper">
        <button
          data-cy="btn-edit"
          class="contact-item__button contact-item__edit-button"
          @click="onEdit"
        >
          Edit
        </button>
        <button
          data-cy="btn-delete"
          class="contact-item__button contact-item__delete-button"
          @click="onDelete"
        >
          Hapus
        </button>
      </div>
    </div>
    <div class="contact-item__second-row">
      <p class="contact-item__phone-email">
        <span data-cy="item-phone">{{ phone_number }}</span> |
        <span data-cy="item-email">{{ email }}</span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ContactItem",
  props: {
    id: Number,
    full_name: String,
    phone_number: String,
    email: String,
  },
  methods: {
    onEdit() {
      this.$parent.setSelectedData(
        this.id,
        this.full_name,
        this.phone_number,
        this.email
      );
    },
    async onDelete() {
      await this.$store.dispatch("deleteContact", this.id);
      this.$parent.getAllContactsData();
    },
  },
};
</script>

<style lang="scss" scoped>
.contact-item {
  &__wrapper {
    margin-bottom: 12px;
    width: 90%;
    height: 48px;
    padding: 24px;
    border-radius: 8px;
    background: #ffffff;
    box-shadow: 0 6px 10px rgb(0 0 0 / 10%);
  }

  &__first-row {
    display: flex;
    justify-content: space-between;
  }

  &__name {
    margin: 0;
  }

  &__phone-email {
    margin: 0;
  }

  &__button-wrapper {
    display: flex;
    gap: 8px;
  }

  &__button {
    min-width: 64px;
    height: 36px;
    padding-left: 12px;
    padding-right: 12px;
    border: none;
    border-radius: 4px;
    font-size: 14px;
    font-weight: bold;
    color: #ffffff;
  }

  &__edit-button {
    background: #16abf8;
  }

  &__delete-button {
    background: #dc3545;
  }
}
</style>
