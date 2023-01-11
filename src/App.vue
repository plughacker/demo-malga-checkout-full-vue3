<template>
  <MalgaCheckoutFull
    :sandbox="true"
    :publicKey="publicKey"
    :clientId="clientId"
    :merchantId="merchantId"
    :paymentMethods="{
      pix: {
        expiresIn: 3600,
      },
      credit: {
        installments: {
          quantity: 1,
          show: true,
        },
        checkedSaveCard: false,
        showCreditCard: true,
      },
      boleto: {
        expiresDate: '2022-12-31',
        instructions: 'Instruções para pagamento do boleto',
        interest: {
          days: 1,
          amount: 100,
        },
        fine: {
          days: 2,
          amount: 200,
        },
      },
    }"
    :transactionConfig="{
      statementDescriptor: '#1 Demonstration Malga Checkout',
      amount: 100,
      description: '',
      orderId: '',
      currency: 'BRL',
      capture: false,
    }"
    :dialogConfig="{
      show: true,
      actionButtonLabel: 'Continuar',
      errorActionButtonLabel: 'Tentar novamente',
      successActionButtonLabel: 'Continuar',
      successRedirectUrl: 'https://www.malga.io/',
    }"
    :pageConfig="{
      footerDescription: 'Todos os direitos reservados © 2023 Malga.',
      backRoute: 'https://www.malga.io/',
      delivery: 0,
      products: [
        {
          name: 'Produto 1',
          quantity: 2,
          amount: 50,
          description: 'Descrição do produto 1',
          sku: '123',
          risk: 'Low',
        },
        {
          name: 'Produto 2',
          quantity: 2,
          amount: 40,
          description: 'Descrição do produto 2',
          sku: '124',
          risk: 'Low',
        },
      ],
    }"
    @transactionSuccess="handlePaymentSuccess"
    @transactionFailed="handlePaymentFailed"
  />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import MalgaCheckoutFull from "@malga-checkout-full/vue";

import {
  MalgaCheckoutFullTransactionSuccessEvent,
  MalgaCheckoutFullTransactionErrorEvent,
} from "./App.types";

export default defineComponent({
  name: "App",
  components: {
    MalgaCheckoutFull,
  },
  data() {
    return {
      publicKey: "<YOUR_PUBLIC_KEY>",
      clientId: "<YOUR_CLIENT_ID>",
      merchantId: "<YOUR_MERCHANT_ID>",
    };
  },
  methods: {
    handlePaymentSuccess(data: MalgaCheckoutFullTransactionSuccessEvent) {
      console.log(data);
    },
    handlePaymentFailed(error: MalgaCheckoutFullTransactionErrorEvent) {
      console.log(error);
    },
  },
});
</script>

<style>
:root {
  /* Colors */
  --malga-checkout-color-page-background: #eef2f6;

  --malga-checkout-color-brand-accent-light: #79dbd4;
  --malga-checkout-color-brand-accent-normal: #39bfad;

  --malga-checkout-color-brand-clean: #c3f4ef;
  --malga-checkout-color-brand-light: #79dbd4;
  --malga-checkout-color-brand-normal: #39bfad;
  --malga-checkout-color-brand-middle: #2fac9b;
  --malga-checkout-color-brand-dark: #147f70;

  --malga-checkout-color-grey-light: #666666;
  --malga-checkout-color-grey-normal: #4d4d4d;
  --malga-checkout-color-grey-middle: #333333;
  --malga-checkout-color-grey-dark: #1a1a1a;
  --malga-checkout-color-grey-darkness: #000000;

  --malga-checkout-color-accent-light: #ffffff;
  --malga-checkout-color-accent-normal: #f1f1f1;
  --malga-checkout-color-accent-middle: #cbcbcb;

  --malga-checkout-color-warning-light: #fff8e6;
  --malga-checkout-color-warning-normal: #f9df8d;
  --malga-checkout-color-warning-middle: #ffa400;

  --malga-checkout-color-modal-success: #00ae42;
  --malga-checkout-color-modal-error: #ed3a3d;
  --malga-checkout-color-modal-neutral: #4d4d4d;
  --malga-checkout-color-modal-action-button-error: #000000;
  --malga-checkout-color-modal-action-button-error-hover: #333333;
  --malga-checkout-color-modal-action-button-success: #000000;
  --malga-checkout-color-modal-action-button-success-hover: #333333;
  --malga-checkout-color-modal-action-button-success-font-color: #ffffff;
  --malga-checkout-color-modal-action-button-error-font-color: #ffffff;

  /* Typography */
  --malga-checkout-typography-family: "Inter", sans-serif;

  /* Spacings */
  --malga-checkout-spacing-xxs: 4px;
  --malga-checkout-spacing-xs: 8px;
  --malga-checkout-spacing-sm: 16px;
  --malga-checkout-spacing-default: 24px;
  --malga-checkout-spacing-md: 32px;
  --malga-checkout-spacing-lg: 48px;
  --malga-checkout-spacing-xlg: 64px;
  --malga-checkout-spacing-xxlg: 96px;

  /* Sizes */
  --malga-checkout-size-min-width: 250px;

  /* Border Radius */
  --malga-checkout-border-radius-default: 4px;
  --malga-checkout-border-radius-md: 6px;
  --malga-checkout-border-radius-lg: 20px;

  /* Transitions Time */
  --malga-checkout-transition-slow: 0.3s;
  --malga-checkout-transition-default: 0.5s;
}

html {
  background: #eef2f6;
}
</style>
