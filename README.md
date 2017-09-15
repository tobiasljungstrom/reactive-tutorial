
difyOfferForEngagement(engagementCategory: string): BaseOption {
    for(const offer of this.offers) {
      for(const option of offer.extraOptions) {
        for(const product of option.products) {
          if(product.productSubCategory === engagementCategory) {
            return option;
          }
        }
      }
    }
  }

And then:

getOptions(id: string): Observable<BaseOption> {
    const allOptions: OptionsResponse[] = [];

    return Observable
      .from(allOptions)
      .flatMap(option => option.extraOptions)
      .filter(extraOption => {
        return this.matchBaseOption(extraOption, id);
      });
  }

  matchBaseOption(option: BaseOption, id: string): boolean {
    return option.products.find(prod => prod.id === id) !== undefined;
  }

