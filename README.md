<!-- RIGHT part (thumbs area) -->
                                        <div class="thumbs-container">
                                            <lightning-button-icon
                                                icon-name="utility:like"
                                                alternative-text="Thumbs Up"
                                                title="Thumbs Up"
                                                variant="bare"
                                                data-action-id={ar.action.Id}
                                                onclick={handleThumbsUp}
                                                class="thumb-btn thumb-up">
                                            </lightning-button-icon>
                                            <lightning-button-icon
                                                icon-name="utility:dislike"
                                                alternative-text="Thumbs Down"
                                                title="Thumbs Down"
                                                variant="bare"
                                                data-action-id={ar.action.Id}
                                                onclick={handleThumbsDown}
                                                class="thumb-btn thumb-down">
                                            </lightning-button-icon>
                                        </div>
