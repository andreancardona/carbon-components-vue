<template>
  <div :class="`cv-definition-tooltip ${carbonPrefix}--tooltip--definition ${carbonPrefix}--tooltip--a11y`" :id="uid">
    <button
      :aria-describedby="`${uid}-label`"
      :class="[
        `${carbonPrefix}--tooltip__trigger`,
        `${carbonPrefix}--tooltip--a11y`,
        `${carbonPrefix}--tooltip__trigger--definition`,
        `${carbonPrefix}--tooltip--${direction}`,
        `${carbonPrefix}--tooltip--align-${alignment}`,
      ]"
      type="button"
    >
      {{ term }}
    </button>
    <div :class="`${carbonPrefix}--assistive-text`" :id="`${uid}-label`" role="tooltip">{{ definition }}</div>
  </div>
</template>

<script>
import { uidMixin, carbonPrefixMixin } from '../../mixins';
import { alignments, directions } from './consts';

export default {
  name: 'CvDefinitionTooltip',
  mixins: [uidMixin, carbonPrefixMixin],
  props: {
    alignment: { type: String, default: 'center', validator: val => alignments.includes(val) },
    definition: { type: String, required: true },
    direction: {
      type: String,
      default: 'top',
      validator: val => {
        const valid = directions.includes(val);
        if (!valid) {
          console.warn(`CVDefinitionTooltip.direction must be one of the following: ${directions}`);
        }
        return valid;
      },
    },
    term: { type: String, required: true },
  },
};
</script>
