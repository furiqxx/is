<template>
  <button 
    :class="[
      $style.button, 
      $style[`button--${props.size}`],
      { [$style['button--rounded']]: props.rounded }
    ]" 
    :data-layout="props.layout" 
    :disabled="props.isDisabled" 
    :type="props.type"
  >
    <slot></slot>
  </button>
</template>

<script setup lang="ts">
interface IProps {
  layout?: 'primary' | 'secondary';
  type?: 'submit' | 'button';
  isDisabled?: boolean;
  size?: 'small' | 'medium' | 'large'; // Добавляем размер
  rounded?: boolean; // Добавляем скругление
}

const props = withDefaults(defineProps<IProps>(), {
  layout: 'primary',
  type: 'button',
  size: 'medium',
  rounded: false,
});
</script>

<style module lang="scss">
.button {
  position: relative;
  display: inline-flex;
  gap: 8px;
  align-items: center;
  justify-content: center;
  height: 40px;
  padding: 16px 32px;
  font-size: 1rem;
  line-height: 1.5;
  color: var(--color-white);
  background: var(--color-primary);
  border-radius: 16px;
  border: 2px solid var(--color-primary);
  transition: all 0.3s ease;
  cursor: pointer;

  &:hover:not(:disabled) {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  }

  &:disabled {
    opacity: 0.6;
    cursor: not-allowed;
  }

  &[data-layout='secondary'] {
    color: var(--color-primary);
    background-color: var(--color-transparent);
    border-color: var(--color-primary);
  }

  // Размеры
  &.button--small {
    height: 32px;
    padding: 8px 16px;
    font-size: 0.875rem;
    border-radius: 12px;
  }

  &.button--medium {
    height: 40px;
    padding: 16px 32px;
    font-size: 1rem;
  }

  &.button--large {
    height: 48px;
    padding: 20px 40px;
    font-size: 1.125rem;
    border-radius: 20px;
  }

  // Скругление
  &.button--rounded {
    border-radius: 50px;
  }
}
</style>