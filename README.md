<!-- Feedback Popover -->
        <template if:true={showFeedbackModal}>
            <div class="feedback-popover slds-popover slds-popover_medium slds-nubbin_bottom-right">
                <div class="slds-popover__header">
                    <h3 class="slds-popover__title">
                        Why wasn't it helpful?
                        <lightning-icon
                            icon-name="utility:info"
                            alternative-text="Your response helps us to improve the model's performance and the user experience"
                            title="Your response helps us to improve the model's performance and the user experience"
                            size="x-small"
                            class="slds-m-left_x-small">
                        </lightning-icon>
                        <lightning-button-icon
                            icon-name="utility:close"
                            onclick={handleCancelFeedback}
                            alternative-text="close"
                            variant="bare"
                            size="x-small"
                            class="slds-m-left_x-small">
                        </lightning-button-icon>
                    </h3>
                </div>
                <div class="slds-popover__body">
                    <div class="slds-form-element">
                        <fieldset class="slds-form-element">
                            <legend class="slds-form-element__legend slds-form-element__label">Select all that apply: <span class="slds-required">*</span></legend>
                            <div class="slds-form-element__control">
                                <template for:each={feedbackOptions} for:item="option">
                                    <div key={option.value} class="slds-checkbox slds-m-bottom_small">
                                        <input 
                                            type="checkbox" 
                                            name="feedback-options"
                                            id={option.value}
                                            value={option.value}
                                            checked={option.checked}
                                            onchange={handleFeedbackOptionChange} />
                                        <label class="slds-checkbox__label" for={option.value}>
                                            <span class="slds-checkbox__faux"></span>
                                            <span class="slds-form-element__label">{option.label}</span>
                                        </label>
                                    </div>
                                </template>
                            </div>
                        </fieldset>
                    </div>
                    
                    <div class="slds-form-element slds-m-top_medium">
                        <label class="slds-form-element__label" for="feedback-textarea">Tell us more</label>
                        <div class="slds-form-element__control">
                            <lightning-textarea
                                id="feedback-textarea"
                                placeholder="Give feedback..."
                                value={feedbackText}
                                onchange={handleFeedbackTextChange}
                                max-length="500">
                            </lightning-textarea>
                        </div>
                    </div>
                </div>
                <div class="slds-popover__footer">
                    <lightning-button
                        variant="neutral"
                        label="Cancel"
                        onclick={handleCancelFeedback}
                        size="small">
                    </lightning-button>
                    <lightning-button
                        variant="brand"
                        label="Submit"
                        onclick={handleSubmitFeedback}
                        size="small">
                    </lightning-button>
                </div>
            </div>
        </template>
