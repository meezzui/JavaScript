ionViewWillEnter() {
    this.userForm = Object.entries(this.userForm).reduce((a, [k, v]) => {
      a[k] = ''
      return a
 }
