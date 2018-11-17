### GPIO Setup & control
In order:
- start by checking the schematic within which the STM32 is & the way buttons/leds connects ( or any other in/out )
- depending on that, in STM32CubeMX > Pinout: click the desired pin(s) & select GPIO_Input or GPIO_Output
- if our GPIOs defaults HIGH, we have to set stuff in STM32CubeMX > Configuration > System > GPIO  
  Ex: for a LED turning ON when the pin is HIGH:  
  - GPIO output level: low ( if the pin is low or high by default )
  - GPIO mode: Output Push Pull ( handle going high & going low )
  - GPIO Pull-up/Pull-down: no pull-up no pull-down ( using external pull's if needed )
  - Maximum outout speed: low ( the smoothness of the pin state change )
  - User Label: EXTLED ( the label which 'll generate a ```#define```statement  )
  Ex: for a LED turning ON when the pin is LOW:  
  - GPIO output level: high ( if the pin is low or high by default )
  - GPIO mode: Output Push Pull ( handle going high & going low )
  - GPIO Pull-up/Pull-down: no pull-up no pull-down ( using external pull's if needed )
  - Maximum outout speed: low ( the smoothness of the pin state change )
  - User Label: LD1 ( the label which 'll generate a ```#define```statement  )
- in case we need to tweak or set the aboves without using STM32CubeMX, remember the aboves writes in the following files:  
  main.h:  
  ```CPP
  #define EXTLED_Pin GPIO_PIN_11
  #define EXTLED_GPIO_Port GPIOD
  #define BTN1_Pin GPIO_PIN_15
  #define BTN1_GPIO_Port GPIOD
  #define LD1_Pin GPIO_PIN_0
  #define LD1_GPIO_Port GPIOE
  ```
  main.c:  
  ```CPP
  static void MX_GPIO_Init(void)
  {

    GPIO_InitTypeDef GPIO_InitStruct;

    /* GPIO Ports Clock Enable */
    __HAL_RCC_GPIOH_CLK_ENABLE();
    __HAL_RCC_GPIOD_CLK_ENABLE();
    __HAL_RCC_GPIOA_CLK_ENABLE();
    __HAL_RCC_GPIOE_CLK_ENABLE();

    /*Configure GPIO pin Output Level */
    HAL_GPIO_WritePin(EXTLED_GPIO_Port, EXTLED_Pin, GPIO_PIN_RESET);

    /*Configure GPIO pin Output Level */
    HAL_GPIO_WritePin(LD1_GPIO_Port, LD1_Pin, GPIO_PIN_SET);

    /*Configure GPIO pin : EXTLED_Pin */
    GPIO_InitStruct.Pin = EXTLED_Pin;
    GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
    GPIO_InitStruct.Pull = GPIO_NOPULL;
    GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
    HAL_GPIO_Init(EXTLED_GPIO_Port, &GPIO_InitStruct);

    /*Configure GPIO pin : BTN1_Pin */
    GPIO_InitStruct.Pin = BTN1_Pin;
    GPIO_InitStruct.Mode = GPIO_MODE_INPUT;
    GPIO_InitStruct.Pull = GPIO_NOPULL;
    HAL_GPIO_Init(BTN1_GPIO_Port, &GPIO_InitStruct);

    /*Configure GPIO pin : LD1_Pin */
    GPIO_InitStruct.Pin = LD1_Pin;
    GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
    GPIO_InitStruct.Pull = GPIO_NOPULL;
    GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
    HAL_GPIO_Init(LD1_GPIO_Port, &GPIO_InitStruct);

  }
  ```
